import { collectSitemap } from './parse.mjs';
import './shared/sitemapd.CGXN3Oad.mjs';
import 'fast-xml-parser';

const DEFAULT_MAX_REDIRECTS = 5;
const DEFAULT_MAX_WIRE_BYTES = 50 * 1024 * 1024;
const DEFAULT_MAX_DEPTH = 3;
const DEFAULT_MAX_DOCUMENTS = 100;
const DEFAULT_MAX_URLS = 5e4;
function parseLimit(value, fallback, name) {
  if (value === void 0)
    return fallback;
  if (!Number.isFinite(value) || value < 0 || !Number.isInteger(value))
    throw new RangeError(`${name} must be a non-negative finite integer`);
  return value;
}
function parseConcurrency(value) {
  if (value === void 0)
    return 1;
  if (!Number.isSafeInteger(value) || value < 1)
    throw new RangeError("concurrency must be a positive safe integer");
  return value;
}
function unique(values) {
  return [...new Set(values)];
}
function parseWalkInput(input) {
  if (typeof input === "string") {
    return [{ url: input, depth: 0, source: "root" }];
  }
  if (input.every((entry) => typeof entry === "string")) {
    return input.map((url) => ({ url, depth: 0, source: "root" }));
  }
  return input.map((entry) => {
    if (entry.source === "root") {
      if (entry.depth !== 0 || entry.parentUrl !== void 0)
        throw new TypeError("A root walk entry must have depth 0 and no parentUrl");
      return { url: entry.url, depth: 0, source: "root" };
    }
    if (!Number.isSafeInteger(entry.depth) || entry.depth < 1)
      throw new RangeError("An index child walk entry must have a positive safe depth");
    if (!entry.parentUrl)
      throw new TypeError("An index child walk entry requires parentUrl");
    return { ...entry };
  });
}
function createSitemapReader(options) {
  const read = async (initialUrl, readOptions = {}) => {
    const maxRedirects = parseLimit(
      readOptions.maxRedirects ?? options.limits?.maxRedirects,
      DEFAULT_MAX_REDIRECTS,
      "maxRedirects"
    );
    const maxWireBytes = parseLimit(
      readOptions.maxWireBytes ?? options.limits?.maxWireBytes,
      DEFAULT_MAX_WIRE_BYTES,
      "maxWireBytes"
    );
    let url = initialUrl;
    let source = readOptions.source ?? "root";
    let parentUrl = readOptions.parentUrl;
    const depth = readOptions.depth ?? 0;
    for (let redirects = 0; redirects <= maxRedirects; redirects++) {
      const request = {
        url,
        resource: "sitemap",
        source,
        depth,
        maxWireBytes,
        ...parentUrl ? { parentUrl } : {},
        ...readOptions.signal ? { signal: readOptions.signal } : {}
      };
      const authorization = await options.authorizeTarget(request);
      if (authorization._tag === "deny") {
        return {
          _tag: "failure",
          url,
          reason: "unauthorized",
          detail: authorization.reason
        };
      }
      const loaded = await options.loadDocument(request);
      if (loaded._tag === "redirect") {
        if (redirects === maxRedirects) {
          return {
            _tag: "failure",
            url,
            reason: "redirect_limit",
            detail: `Sitemap exceeds ${maxRedirects} redirects`
          };
        }
        let redirected;
        try {
          redirected = new URL(loaded.location, url).toString();
        } catch {
          return {
            _tag: "failure",
            url,
            reason: "invalid_redirect",
            detail: `Invalid redirect location: ${loaded.location}`
          };
        }
        parentUrl = url;
        url = redirected;
        source = "redirect";
        continue;
      }
      if (loaded._tag === "not_found")
        return loaded;
      if (loaded._tag === "http_error") {
        return {
          _tag: "failure",
          url,
          reason: "http",
          detail: `HTTP ${loaded.status}: ${loaded.statusText}`,
          status: loaded.status
        };
      }
      if (loaded._tag === "load_error") {
        return {
          _tag: "failure",
          url,
          reason: "load",
          code: loaded.code,
          detail: loaded.detail
        };
      }
      const maxDecodedBytes = readOptions.maxDecodedBytes ?? options.limits?.maxDecodedBytes;
      const maxEntries = readOptions.maxEntries ?? options.limits?.maxEntries;
      const parsed = await collectSitemap(loaded.body, {
        ...readOptions.formatHint ? { formatHint: readOptions.formatHint } : {},
        ...maxDecodedBytes !== void 0 ? { maxDecodedBytes } : {},
        ...maxEntries !== void 0 ? { maxEntries } : {}
      });
      if (parsed._tag !== "document") {
        return {
          _tag: "failure",
          url,
          reason: "document",
          detail: parsed.issues.map((issue) => issue.message).join("; ") || parsed.completeness._tag
        };
      }
      return { _tag: "ok", url: loaded.url, document: parsed.document, parse: parsed };
    }
    throw new Error("Unreachable redirect loop state");
  };
  async function walk(input, walkOptions = {}) {
    const maxDepth = parseLimit(
      walkOptions.maxDepth ?? options.limits?.maxDepth,
      DEFAULT_MAX_DEPTH,
      "maxDepth"
    );
    const maxDocuments = parseLimit(
      walkOptions.maxDocuments ?? options.limits?.maxDocuments,
      DEFAULT_MAX_DOCUMENTS,
      "maxDocuments"
    );
    const maxUrls = parseLimit(
      walkOptions.maxUrls ?? options.limits?.maxUrls,
      DEFAULT_MAX_URLS,
      "maxUrls"
    );
    const concurrency = parseConcurrency(walkOptions.concurrency);
    const retainEntries = walkOptions.retention !== "none";
    const queue = parseWalkInput(input);
    const seenDocuments = new Set(walkOptions.seenDocuments ?? []);
    const seenUrls = retainEntries ? /* @__PURE__ */ new Set() : null;
    const entries = [];
    const references = [];
    const failures = [];
    const reasons = [];
    const active = /* @__PURE__ */ new Map();
    const settled = /* @__PURE__ */ new Map();
    const scheduled = /* @__PURE__ */ new Map();
    const interrupted = [];
    const controller = new AbortController();
    const callerSignal = walkOptions.signal;
    const abortFromCaller = () => {
      if (!controller.signal.aborted) {
        controller.abort(
          callerSignal?.reason ?? new DOMException("Sitemap traversal was cancelled", "AbortError")
        );
      }
    };
    if (callerSignal?.aborted)
      abortFromCaller();
    else
      callerSignal?.addEventListener("abort", abortFromCaller, { once: true });
    let urlsObserved = 0;
    let referencesObserved = 0;
    let documentsAttempted = 0;
    let documentsRead = 0;
    let nextSequence = 0;
    let nextCommit = 0;
    let schedulingStopped = false;
    const hasQueuedDocument = () => queue.some((item) => !seenDocuments.has(item.url));
    const stopAndDrain = async (reason, preserveFrontier = false) => {
      schedulingStopped = true;
      if (!controller.signal.aborted)
        controller.abort(reason);
      if (preserveFrontier) {
        interrupted.push(
          ...[...scheduled.entries()].sort(([left], [right]) => left - right).map(([, item]) => item)
        );
      }
      const pending = [...active.values()];
      active.clear();
      settled.clear();
      scheduled.clear();
      await Promise.all(pending);
    };
    const fill = () => {
      while (!schedulingStopped && !controller.signal.aborted && active.size + settled.size < concurrency) {
        let next;
        while (queue.length > 0) {
          const candidate = queue.shift();
          if (seenDocuments.has(candidate.url))
            continue;
          next = candidate;
          break;
        }
        if (!next)
          return;
        if (documentsAttempted >= maxDocuments) {
          queue.unshift(next);
          reasons.push("document_limit");
          schedulingStopped = true;
          return;
        }
        seenDocuments.add(next.url);
        documentsAttempted++;
        const sequence = nextSequence++;
        const promise = read(next.url, {
          ...walkOptions,
          signal: controller.signal,
          source: next.source,
          depth: next.depth,
          ...next.parentUrl ? { parentUrl: next.parentUrl } : {}
        }).then(
          (result) => ({
            _tag: "result",
            sequence,
            item: next,
            result
          }),
          (error) => ({
            _tag: "thrown",
            sequence,
            item: next,
            error
          })
        );
        active.set(sequence, promise);
        scheduled.set(sequence, next);
      }
    };
    const visit = async (item, result) => {
      if (!walkOptions.onDocument)
        return;
      const document = {
        requestedUrl: item.url,
        resolvedUrl: result.url,
        source: item.source,
        depth: item.depth,
        ...item.parentUrl ? { parentUrl: item.parentUrl } : {},
        document: result.document,
        parse: result.parse
      };
      const visitation = await Promise.resolve().then(() => walkOptions.onDocument(document)).then(
        () => ({ _tag: "ok" }),
        (error) => ({ _tag: "failure", error })
      );
      if (visitation._tag === "failure") {
        await stopAndDrain(visitation.error);
        throw visitation.error;
      }
    };
    try {
      while (true) {
        if (callerSignal?.aborted) {
          reasons.push("cancelled");
          await stopAndDrain(
            callerSignal.reason ?? new DOMException("Sitemap traversal was cancelled", "AbortError"),
            true
          );
          break;
        }
        fill();
        const next = settled.get(nextCommit);
        if (!next) {
          if (active.size === 0)
            break;
          const completed = await Promise.race(active.values());
          active.delete(completed.sequence);
          settled.set(completed.sequence, completed);
          continue;
        }
        settled.delete(nextCommit);
        scheduled.delete(nextCommit);
        nextCommit++;
        if (next._tag === "thrown") {
          await stopAndDrain(next.error);
          throw next.error;
        }
        const { item, result } = next;
        if (result._tag !== "ok") {
          failures.push({ ...item, result });
          reasons.push("read_failure");
          continue;
        }
        documentsRead++;
        if (result.parse.completeness._tag === "partial")
          reasons.push("document_partial");
        if (result.document._tag === "index") {
          const childUrls = result.document.entries.map((entry) => entry.loc);
          referencesObserved += childUrls.length;
          if (retainEntries)
            references.push(...result.document.entries);
          await visit(item, result);
          if (item.depth >= maxDepth && childUrls.length > 0) {
            reasons.push("depth_limit");
            continue;
          }
          for (const url of childUrls) {
            queue.push({
              url,
              depth: item.depth + 1,
              source: "index_child",
              parentUrl: result.url
            });
          }
          continue;
        }
        const documentUrlCount = result.document.entries.length;
        if (urlsObserved + documentUrlCount > maxUrls) {
          urlsObserved += documentUrlCount;
          reasons.push("url_limit");
          await stopAndDrain(
            new DOMException("Sitemap traversal reached its URL limit", "AbortError"),
            true
          );
          break;
        }
        urlsObserved += documentUrlCount;
        if (retainEntries) {
          for (const entry of result.document.entries) {
            if (seenUrls.has(entry.loc))
              continue;
            seenUrls.add(entry.loc);
            entries.push(entry);
          }
        }
        await visit(item, result);
        if (urlsObserved >= maxUrls && (active.size > 0 || settled.size > 0 || hasQueuedDocument())) {
          reasons.push("url_limit");
          await stopAndDrain(
            new DOMException("Sitemap traversal reached its URL limit", "AbortError"),
            true
          );
          break;
        }
      }
    } finally {
      callerSignal?.removeEventListener("abort", abortFromCaller);
    }
    const retention = retainEntries ? {
      entriesRetained: true,
      entries,
      references
    } : {
      entriesRetained: false,
      entries: [],
      references: []
    };
    const data = {
      ...retention,
      urlsObserved,
      referencesObserved,
      documentsAttempted,
      documentsRead,
      failures,
      frontier: (() => {
        const urls = /* @__PURE__ */ new Set();
        const result = [];
        for (const entry of interrupted) {
          if (urls.has(entry.url))
            continue;
          urls.add(entry.url);
          result.push(entry);
        }
        for (const entry of queue) {
          if (seenDocuments.has(entry.url) || urls.has(entry.url))
            continue;
          urls.add(entry.url);
          result.push(entry);
        }
        return result;
      })()
    };
    const partialReasons = unique(reasons);
    return partialReasons.length > 0 ? { _tag: "partial", reasons: partialReasons, ...data } : { _tag: "complete", ...data };
  }
  return { read, walk };
}

function parseRobotsSitemaps(input, baseUrl) {
  const entries = [];
  const seen = /* @__PURE__ */ new Set();
  for (const match of input.matchAll(/^\s*sitemap\s*:\s*(\S+)\s*$/gim)) {
    const raw = match[1];
    if (!raw)
      continue;
    let loc = raw;
    if (baseUrl) {
      try {
        loc = new URL(raw, baseUrl).toString();
      } catch {
        continue;
      }
    }
    if (seen.has(loc))
      continue;
    seen.add(loc);
    entries.push({ loc });
  }
  return entries;
}

export { createSitemapReader, parseRobotsSitemaps };
