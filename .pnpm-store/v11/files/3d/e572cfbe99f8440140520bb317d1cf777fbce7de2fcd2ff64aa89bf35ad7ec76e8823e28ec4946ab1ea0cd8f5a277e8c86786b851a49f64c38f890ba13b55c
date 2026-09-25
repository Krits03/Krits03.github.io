import { parseSitemap } from 'sitemapd/parse';
export { collectSitemap, parseSitemap } from 'sitemapd/parse';
export { p as parseHtmlExtractSitemapMeta } from './shared/sitemap.BoMnWHOt.mjs';
export { createSitemapReader } from 'sitemapd';
export { createFetchDocumentLoader } from 'sitemapd/fetch';
import 'ufo';
import 'ultrahtml';

const CHANGE_FREQUENCIES = /* @__PURE__ */ new Set([
  "always",
  "hourly",
  "daily",
  "weekly",
  "monthly",
  "yearly",
  "never"
]);
function legacyWarning(issue, kind) {
  if (issue.code === "missing_loc") {
    return {
      type: "validation",
      message: kind === "index" ? "Sitemap entry missing required loc element" : "URL entry missing required loc element",
      ...kind === "urlset" ? { context: { url: "undefined" } } : {}
    };
  }
  if (issue.code === "invalid_loc" && kind === "index") {
    const url = String(issue.value);
    if (URL.canParse(url))
      return void 0;
    return {
      type: "validation",
      message: "Sitemap entry has invalid URL",
      context: { url }
    };
  }
  if (issue.severity !== "warning" || issue.code === "invalid_loc")
    return void 0;
  return {
    type: "validation",
    message: issue.message,
    ...issue.field || issue.value !== void 0 ? {
      context: {
        ...issue.field ? { field: issue.field } : {},
        ...issue.value !== void 0 ? { value: issue.value } : {}
      }
    } : {}
  };
}
function legacyImages(images) {
  return images?.map((image) => ({
    loc: image.loc,
    ...image.caption ? { caption: image.caption } : {},
    ...image.geoLocation ? { geo_location: image.geoLocation } : {},
    ...image.title ? { title: image.title } : {},
    ...image.license ? { license: image.license } : {}
  }));
}
function legacyUrl(entry) {
  const warnings = [];
  const url = { loc: entry.loc };
  if (entry.lastmod)
    url.lastmod = entry.lastmod;
  if (entry.changefreq) {
    if (CHANGE_FREQUENCIES.has(entry.changefreq)) {
      url.changefreq = entry.changefreq;
    } else {
      warnings.push({
        type: "validation",
        message: "Invalid changefreq value",
        context: { url: entry.loc, field: "changefreq", value: entry.changefreq }
      });
    }
  }
  if (entry.priority !== void 0) {
    const priority = Number.parseFloat(entry.priority);
    if (Number.isNaN(priority)) {
      warnings.push({
        type: "validation",
        message: "Invalid priority value",
        context: { url: entry.loc, field: "priority", value: entry.priority }
      });
    } else {
      if (priority < 0 || priority > 1) {
        warnings.push({
          type: "validation",
          message: "Priority value should be between 0.0 and 1.0, clamping to valid range",
          context: { url: entry.loc, field: "priority", value: priority }
        });
      }
      url.priority = Math.max(0, Math.min(1, priority));
    }
  }
  const extensions = entry.extensions;
  if (extensions?.alternatives) {
    url.alternatives = extensions.alternatives.flatMap((alternative) => {
      if ((!alternative.rel || alternative.rel === "alternate") && alternative.hreflang)
        return [{ hreflang: alternative.hreflang, href: alternative.href }];
      warnings.push({
        type: "validation",
        message: 'Alternative link missing required rel="alternate", hreflang, or href',
        context: { url: entry.loc, field: "link" }
      });
      return [];
    });
  }
  const images = legacyImages(extensions?.images);
  if (images?.length)
    url.images = images;
  if (extensions?.videos?.length)
    url.videos = extensions.videos;
  if (extensions?.news)
    url.news = extensions.news;
  return { url, warnings };
}
function positiveOption(value, name) {
  if (value === void 0)
    return void 0;
  if (!Number.isSafeInteger(value) || value < 1)
    throw new TypeError(`${name} must be a positive safe integer`);
  return value;
}
function parserFailure(issue, kind, options) {
  if (issue?.code === "empty")
    return new Error("Empty XML input provided");
  if (issue?.code === "decoded_limit" && options.maxBufferBytes)
    return new Error(`Sitemap XML buffer exceeds maxBufferBytes of ${options.maxBufferBytes}`);
  const entryLimit = issue?.message.match(/^Sitemap entry exceeds (\d+) bytes$/);
  if (entryLimit)
    return new Error(`Sitemap entry exceeds maxEntryBytes of ${entryLimit[1]}`);
  if (issue?.code === "unsupported" || issue?.code === "html") {
    return new Error(
      kind === "index" ? "XML does not contain a valid sitemapindex element" : kind === "urlset" ? "XML does not contain a valid urlset element" : "XML does not contain a valid sitemap element"
    );
  }
  return new Error(`Failed to parse XML: ${issue?.message || "Malformed sitemap"}`);
}
async function* parseSitemapStreamInternal(input, options = {}, expectedKind) {
  const maxEntryBytes = positiveOption(options.maxEntryBytes, "maxEntryBytes");
  const maxBufferBytes = positiveOption(options.maxBufferBytes, "maxBufferBytes");
  let kind;
  let lastIssue;
  let invalidUrlEntries = 0;
  let validUrls = 0;
  for await (const event of parseSitemap(input, {
    ...maxEntryBytes ? { maxEntryBytes } : {},
    ...maxBufferBytes ? { maxDecodedBytes: maxBufferBytes } : {}
  })) {
    if (event._tag === "document") {
      if (event.format !== "xml") {
        throw new Error(
          expectedKind === "index" ? "XML does not contain a valid sitemapindex element" : expectedKind === "urlset" ? "XML does not contain a valid urlset element" : "XML does not contain a valid sitemap element"
        );
      }
      kind = event.kind;
      yield { _tag: "kind", kind };
    } else if (event._tag === "issue") {
      lastIssue = event.issue;
      if (!kind)
        continue;
      if (event.issue.code === "missing_loc" && kind === "urlset")
        invalidUrlEntries++;
      const warning = legacyWarning(event.issue, kind);
      if (warning)
        yield { _tag: "warning", warning };
    } else if (event._tag === "url") {
      validUrls++;
      const mapped = legacyUrl(event.entry);
      for (const warning of mapped.warnings)
        yield { _tag: "warning", warning };
      yield { _tag: "url", url: mapped.url };
    } else if (event._tag === "sitemap") {
      if (!URL.canParse(event.entry.loc))
        continue;
      yield { _tag: "sitemap", sitemap: event.entry };
    } else if (event.completeness._tag !== "complete") {
      throw parserFailure(lastIssue, kind || expectedKind, options);
    }
  }
  if (kind === "urlset" && invalidUrlEntries > 0 && validUrls === 0) {
    yield {
      _tag: "warning",
      warning: {
        type: "validation",
        message: "No valid URLs found in sitemap after validation"
      }
    };
  }
}
async function* parseSitemapStream(input, options = {}) {
  yield* parseSitemapStreamInternal(input, options);
}
async function* parseSitemapXmlStream(input, options = {}) {
  for await (const event of parseSitemapStreamInternal(input, options, "urlset")) {
    if (event._tag === "kind") {
      if (event.kind !== "urlset")
        throw new Error("XML does not contain a valid urlset element");
      continue;
    }
    if (event._tag !== "sitemap")
      yield event;
  }
}
async function* parseSitemapIndexStream(input, options = {}) {
  for await (const event of parseSitemapStreamInternal(input, options, "index")) {
    if (event._tag === "kind") {
      if (event.kind !== "index")
        throw new Error("XML does not contain a valid sitemapindex element");
      continue;
    }
    if (event._tag !== "url")
      yield event;
  }
}
async function parseSitemapXml(xml) {
  const urls = [];
  const warnings = [];
  for await (const event of parseSitemapXmlStream(xml)) {
    if (event._tag === "url")
      urls.push(event.url);
    else
      warnings.push(event.warning);
  }
  return { urls, warnings };
}
async function parseSitemapIndex(xml) {
  const entries = [];
  const warnings = [];
  for await (const event of parseSitemapIndexStream(xml)) {
    if (event._tag === "sitemap")
      entries.push(event.sitemap);
    else
      warnings.push(event.warning);
  }
  return { entries, warnings };
}
function isSitemapIndex(xml) {
  return xml.includes("<sitemapindex") || xml.includes("sitemapindex>");
}

export { isSitemapIndex, parseSitemapIndex, parseSitemapIndexStream, parseSitemapStream, parseSitemapXml, parseSitemapXmlStream };
