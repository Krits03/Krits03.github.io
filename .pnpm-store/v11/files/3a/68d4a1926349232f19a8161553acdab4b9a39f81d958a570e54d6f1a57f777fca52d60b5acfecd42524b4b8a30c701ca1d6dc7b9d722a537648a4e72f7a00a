import { defu } from "defu";
import { $fetch } from "ofetch";
import { collectSitemap } from "sitemapd/parse";
import { parseURL } from "ufo";
import { getHeader, getRequestHost } from "#nuxtseo/h3";
import { defineCachedFunction, fetchWithEvent } from "#nuxtseo/nitro";
import staticConfig from "#sitemap-virtual/static-config.mjs";
import { logger } from "../../../utils-pure.js";
const changeFrequencies = /* @__PURE__ */ new Set([
  "always",
  "hourly",
  "daily",
  "weekly",
  "monthly",
  "yearly",
  "never"
]);
function readerEntryToSitemapInput(entry) {
  const priority = entry.priority === void 0 ? void 0 : Number.parseFloat(entry.priority);
  const changefreq = entry.changefreq && changeFrequencies.has(entry.changefreq) ? entry.changefreq : void 0;
  return {
    loc: entry.loc,
    ...entry.lastmod ? { lastmod: entry.lastmod } : {},
    ...changefreq ? { changefreq } : {},
    ...priority !== void 0 && Number.isFinite(priority) ? { priority } : {},
    ...entry.extensions?.alternatives ? { alternatives: entry.extensions.alternatives.map(({ hreflang, href }) => ({ hreflang, href })) } : {},
    ...entry.extensions?.images ? {
      images: entry.extensions.images.map((image) => ({
        loc: image.loc,
        ...image.caption ? { caption: image.caption } : {},
        ...image.geoLocation ? { geo_location: image.geoLocation } : {},
        ...image.title ? { title: image.title } : {},
        ...image.license ? { license: image.license } : {}
      }))
    } : {},
    ...entry.extensions?.videos ? { videos: entry.extensions.videos } : {},
    ...entry.extensions?.news ? { news: entry.extensions.news } : {}
  };
}
export function normalizeSourceInput(source) {
  if (typeof source === "string") {
    return { context: { name: "hook" }, fetch: source };
  }
  if (Array.isArray(source)) {
    return { context: { name: "hook" }, fetch: source };
  }
  return source;
}
async function tryFetchWithFallback(url, options, event) {
  const isExternalUrl = !url.startsWith("/");
  if (isExternalUrl) {
    const strategies = [
      // Strategy 1: Use globalThis.$fetch (original approach)
      () => globalThis.$fetch(url, options),
      // Strategy 2: If event is available, try using event context even for external URLs
      event ? () => fetchWithEvent(event, url, options) : null,
      // Strategy 3: Use native fetch as last resort
      () => $fetch(url, options)
    ].filter(Boolean);
    let lastError = null;
    for (const strategy of strategies) {
      try {
        return await strategy();
      } catch (error) {
        lastError = error;
        continue;
      }
    }
    throw lastError;
  }
  return event ? await fetchWithEvent(event, url, options) : await globalThis.$fetch(url, options);
}
const SOURCE_FETCH_MEMO_KEY = "_sitemapSourceFetches";
const SERVER_CACHE_MAX_AGE = staticConfig.cacheMaxAgeSeconds || 60 * 10;
const prerenderSourceFetches = import.meta.prerender ? /* @__PURE__ */ new Map() : void 0;
function useSourceFetchMemo(event) {
  if (import.meta.prerender)
    return prerenderSourceFetches;
  const context = event?.context;
  if (!context)
    return void 0;
  const existing = context[SOURCE_FETCH_MEMO_KEY];
  if (existing)
    return existing;
  const memo = /* @__PURE__ */ new Map();
  context[SOURCE_FETCH_MEMO_KEY] = memo;
  return memo;
}
function hashCacheKey(key) {
  let h1 = 3735928559;
  let h2 = 1103547991;
  for (let i = 0; i < key.length; i++) {
    const ch = key.charCodeAt(i);
    h1 = Math.imul(h1 ^ ch, 2654435761);
    h2 = Math.imul(h2 ^ ch, 1597334677);
  }
  h1 = Math.imul(h1 ^ h1 >>> 16, 2246822507) ^ Math.imul(h2 ^ h2 >>> 13, 3266489909);
  h2 = Math.imul(h2 ^ h2 >>> 16, 2246822507) ^ Math.imul(h1 ^ h1 >>> 13, 3266489909);
  return (4294967296 * (2097151 & h2) + (h1 >>> 0)).toString(36);
}
const fetchSourceUrlsCached = defineCachedFunction(
  (event, _key, url, options) => fetchSourceUrls(url, options, event),
  {
    name: "sitemap:source-urls",
    group: "sitemap",
    base: "sitemap",
    maxAge: SERVER_CACHE_MAX_AGE,
    getKey: (event, key) => {
      const host = getHeader(event, "host") || getHeader(event, "x-forwarded-host") || "";
      const proto = getHeader(event, "x-forwarded-proto") || "https";
      return `source-${proto}-${host}-${hashCacheKey(key)}`;
    },
    swr: true,
    // A failed fetch must never be served again, otherwise one outage empties the sitemap for a
    // whole cache window.
    validate: (entry) => {
      const value = entry.value;
      return value !== void 0 && !value._isFailure;
    }
  }
);
function isSourceCacheEnabled() {
  if (import.meta.dev || import.meta.prerender)
    return false;
  const cacheMaxAgeSeconds = staticConfig.cacheMaxAgeSeconds;
  return typeof cacheMaxAgeSeconds === "number" && cacheMaxAgeSeconds > 0;
}
export async function fetchDataSource(input, event) {
  const context = typeof input.context === "string" ? { name: input.context } : input.context || { name: "fetch" };
  const url = typeof input.fetch === "string" ? input.fetch : input.fetch[0];
  const options = typeof input.fetch === "string" ? {} : input.fetch[1];
  const memo = useSourceFetchMemo(event);
  const key = `${url}::${JSON.stringify(options || {})}`;
  let request = memo?.get(key);
  if (!request) {
    request = event && isSourceCacheEnabled() ? fetchSourceUrlsCached(event, key, url, options) : fetchSourceUrls(url, options, event);
    memo?.set(key, request);
  }
  const result = await request;
  if (result._isFailure)
    memo?.delete(key);
  return { ...input, context, ...result };
}
async function fetchSourceUrls(url, options, event) {
  const start = Date.now();
  const isExternalUrl = !url.startsWith("/");
  const timeout = isExternalUrl ? 1e4 : options.timeout || 5e3;
  const timeoutController = new AbortController();
  const abortRequestTimeout = setTimeout(() => timeoutController.abort(), timeout);
  try {
    let isMaybeErrorResponse = false;
    const pathname = parseURL(url).pathname.toLowerCase();
    const isGzUrl = pathname.endsWith(".gz");
    const isXmlRequest = pathname.endsWith(".xml") || isGzUrl;
    const mergedHeaders = defu(
      options?.headers,
      {
        Accept: isXmlRequest ? "text/xml" : "application/json"
      },
      event && !isExternalUrl ? { host: getRequestHost(event, { xForwardedHost: true }) } : {}
    );
    const fetchOptions = {
      ...options,
      // Fetch XML sources as raw bytes so we can detect and decompress a gzip body
      // (either a `.gz` URL, or a server that serves gzip without Content-Encoding)
      // before it's mangled by a UTF-8 text decode.
      responseType: isXmlRequest ? "arrayBuffer" : "json",
      signal: timeoutController.signal,
      headers: mergedHeaders,
      // Use ofetch's built-in retry for external sources
      ...isExternalUrl && {
        retry: 2,
        retryDelay: 200
      },
      // @ts-expect-error untyped
      onResponse({ response }) {
        if (typeof response._data === "string" && response._data.startsWith("<!DOCTYPE html>"))
          isMaybeErrorResponse = true;
      }
    };
    const res = await tryFetchWithFallback(url, fetchOptions, event);
    const timeTakenMs = Date.now() - start;
    if (isMaybeErrorResponse) {
      return {
        urls: [],
        timeTakenMs,
        error: "Received HTML response instead of JSON",
        // An HTML page is usually an outage or an auth wall, both transient. Treat it like a
        // failed fetch so the empty result is never cached.
        _isFailure: true
      };
    }
    let urls = [];
    if (isXmlRequest) {
      const bytes = res instanceof Uint8Array ? res : new Uint8Array(res);
      const result = await collectSitemap(bytes);
      if (result._tag !== "document")
        throw new Error(result.issues.map((issue) => issue.message).join("; ") || "Invalid sitemap document");
      if (result.document._tag !== "urlset")
        throw new Error("Sitemap URL source must be a URL set, not a sitemap index");
      urls = result.document.entries.map(readerEntryToSitemapInput);
    } else if (typeof res === "object") {
      urls = res.urls || res;
    }
    return {
      timeTakenMs,
      urls
    };
  } catch (_err) {
    const error = _err;
    if (isExternalUrl) {
      const errorInfo = {
        url,
        timeout,
        error: error.message,
        statusCode: error.response?.status,
        statusText: error.response?.statusText,
        method: options?.method || "GET"
      };
      logger.error("Failed to fetch external source.", errorInfo);
    } else {
      logger.error("Failed to fetch source.", { url, error: error.message });
    }
    return {
      urls: [],
      error: error.message,
      _isFailure: true
      // Mark as failure to prevent caching
    };
  } finally {
    if (abortRequestTimeout) {
      clearTimeout(abortRequestTimeout);
    }
  }
}
export async function globalSitemapSources() {
  if (import.meta.prerender) {
    const { readSourcesFromFilesystem } = await import("#sitemap-virtual/read-sources.mjs");
    const sources = await readSourcesFromFilesystem("global-sources.json");
    if (sources) {
      return [...sources];
    }
  }
  const m = await import("#sitemap-virtual/global-sources.mjs");
  return [...m.sources];
}
export async function childSitemapSources(definition) {
  if (definition?.sources?.length)
    return [...definition.sources];
  if (definition?.urls) {
    const urls = typeof definition.urls === "function" ? await definition.urls() : definition.urls;
    return [{
      context: { name: `sitemaps:${definition.sitemapName}:urls`, description: "Set with the sitemap definition `urls`." },
      urls
    }];
  }
  if (!definition?._hasSourceChunk)
    return [];
  if (import.meta.prerender) {
    const { readSourcesFromFilesystem } = await import("#sitemap-virtual/read-sources.mjs");
    const allSources = await readSourcesFromFilesystem("child-sources.json");
    if (allSources) {
      return [...allSources[definition.sitemapName] || []];
    }
  }
  const m = await import("#sitemap-virtual/child-sources.mjs");
  return [...m.sources[definition.sitemapName] || []];
}
export async function resolveSitemapSources(sources, event) {
  return await Promise.all(
    sources.map((source) => {
      const normalized = normalizeSourceInput(source);
      if ("urls" in normalized) {
        return {
          timeTakenMs: 0,
          ...normalized,
          urls: normalized.urls
        };
      }
      if (normalized.fetch)
        return fetchDataSource(normalized, event);
      return {
        ...normalized,
        error: "Invalid source"
      };
    })
  );
}
