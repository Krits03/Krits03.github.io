import { d as decodedTextChunks, i as isSitemapInputFailure } from './shared/sitemapd.CGXN3Oad.mjs';
import { XMLValidator, XMLParser } from 'fast-xml-parser';

const ARRAY_TAGS = /* @__PURE__ */ new Set([
  "url",
  "sitemap",
  "item",
  "entry",
  "image:image",
  "video:video",
  "xhtml:link",
  "link",
  "media:content",
  "media:thumbnail"
]);
const LOC_OPEN = "<loc>";
const LOC_CLOSE = "</loc>";
const LASTMOD_OPEN = "<lastmod>";
const LASTMOD_CLOSE = "</lastmod>";
const CHANGEFREQ_OPEN = "<changefreq>";
const CHANGEFREQ_CLOSE = "</changefreq>";
const PRIORITY_OPEN = "<priority>";
const PRIORITY_CLOSE = "</priority>";
const parser = new XMLParser({
  ignoreAttributes: false,
  attributeNamePrefix: "",
  parseAttributeValue: false,
  parseTagValue: false,
  trimValues: true,
  isArray: (name) => ARRAY_TAGS.has(name)
});
function localName(name) {
  return name.includes(":") ? name.slice(name.lastIndexOf(":") + 1) : name;
}
function child(node, name) {
  if (!node || typeof node !== "object")
    return void 0;
  const record = node;
  if (name in record)
    return record[name];
  for (const key in record) {
    if (localName(key) === name)
      return record[key];
  }
  return void 0;
}
function many(node, name) {
  const value = child(node, name);
  if (value === void 0)
    return [];
  return Array.isArray(value) ? value : [value];
}
function text(value) {
  if (Array.isArray(value))
    return value.length === 1 ? text(value[0]) : void 0;
  if (typeof value === "string" && value.length > 0)
    return value;
  if (typeof value === "number")
    return String(value);
  if (value && typeof value === "object") {
    const raw = value["#text"];
    if (typeof raw === "string" && raw.length > 0)
      return raw;
  }
  return void 0;
}
function attribute(node, name) {
  if (!node || typeof node !== "object")
    return void 0;
  const value = node[name];
  if (Array.isArray(value))
    return value.length === 1 ? text(value[0]) : void 0;
  return typeof value === "string" && value.length > 0 ? value : void 0;
}
function issueForLoc(loc, entryIndex) {
  if (!loc) {
    return {
      code: "missing_loc",
      severity: "warning",
      message: "Sitemap entry is missing its required location",
      entryIndex,
      field: "loc"
    };
  }
  let valid = false;
  try {
    const url = new URL(loc);
    valid = url.protocol === "http:" || url.protocol === "https:";
  } catch {
    valid = false;
  }
  if (!valid) {
    return {
      code: "invalid_loc",
      severity: "warning",
      message: "Sitemap entry location is not an absolute URL",
      entryIndex,
      field: "loc",
      value: loc
    };
  }
  return void 0;
}
function simpleText(value) {
  const trimmed = value?.trim();
  return trimmed || void 0;
}
function hasInvalidXmlText(value) {
  if (value.includes("]]>"))
    return true;
  for (let index = 0; index < value.length; index++) {
    const code = value.charCodeAt(index);
    if (code <= 8 || code === 11 || code === 12 || code >= 14 && code <= 31 || code >= 65534)
      return true;
  }
  return false;
}
function skipXmlWhitespace(input, start) {
  let cursor = start;
  while (cursor < input.length) {
    const code = input.charCodeAt(cursor);
    if (code !== 32 && code !== 9 && code !== 10 && code !== 13)
      break;
    cursor++;
  }
  return cursor;
}
function simpleFieldEnd(input, start, open, close) {
  if (!input.startsWith(open, start))
    return -1;
  const valueStart = start + open.length;
  const end = input.indexOf(close, valueStart);
  if (end === -1)
    return -1;
  const value = input.slice(valueStart, end);
  return value.includes("<") || value.includes("&") || value.includes("\r") || hasInvalidXmlText(value) ? -1 : end;
}
function parseSimpleRecord(xml, recordTag) {
  if (recordTag !== "url" && recordTag !== "sitemap")
    return void 0;
  const recordOpen = recordTag === "url" ? "<url>" : "<sitemap>";
  const recordClose = recordTag === "url" ? "</url>" : "</sitemap>";
  if (!xml.startsWith(recordOpen))
    return void 0;
  let cursor = skipXmlWhitespace(xml, recordOpen.length);
  const locEnd = simpleFieldEnd(xml, cursor, LOC_OPEN, LOC_CLOSE);
  if (locEnd === -1)
    return void 0;
  const loc = simpleText(xml.slice(cursor + LOC_OPEN.length, locEnd));
  cursor = skipXmlWhitespace(xml, locEnd + LOC_CLOSE.length);
  let lastmod;
  if (xml.startsWith(LASTMOD_OPEN, cursor)) {
    const lastmodEnd = simpleFieldEnd(xml, cursor, LASTMOD_OPEN, LASTMOD_CLOSE);
    if (lastmodEnd === -1)
      return void 0;
    lastmod = simpleText(xml.slice(cursor + LASTMOD_OPEN.length, lastmodEnd));
    cursor = skipXmlWhitespace(xml, lastmodEnd + LASTMOD_CLOSE.length);
  }
  let changefreq;
  if (recordTag === "url" && xml.startsWith(CHANGEFREQ_OPEN, cursor)) {
    const changefreqEnd = simpleFieldEnd(xml, cursor, CHANGEFREQ_OPEN, CHANGEFREQ_CLOSE);
    if (changefreqEnd === -1)
      return void 0;
    changefreq = simpleText(xml.slice(cursor + CHANGEFREQ_OPEN.length, changefreqEnd));
    cursor = skipXmlWhitespace(xml, changefreqEnd + CHANGEFREQ_CLOSE.length);
  }
  let priority;
  if (recordTag === "url" && xml.startsWith(PRIORITY_OPEN, cursor)) {
    const priorityEnd = simpleFieldEnd(xml, cursor, PRIORITY_OPEN, PRIORITY_CLOSE);
    if (priorityEnd === -1)
      return void 0;
    priority = simpleText(xml.slice(cursor + PRIORITY_OPEN.length, priorityEnd));
    cursor = skipXmlWhitespace(xml, priorityEnd + PRIORITY_CLOSE.length);
  }
  if (!xml.startsWith(recordClose, cursor) || cursor + recordClose.length !== xml.length)
    return void 0;
  const locIssue = issueForLoc(loc, 0);
  const issues = locIssue ? [locIssue] : [];
  if (recordTag === "sitemap") {
    return {
      _tag: "index",
      format: "xml",
      entries: loc ? [{ loc, ...lastmod ? { lastmod } : {} }] : [],
      issues
    };
  }
  return {
    _tag: "urlset",
    format: "xml",
    entries: loc ? [{
      loc,
      ...lastmod ? { lastmod } : {},
      ...changefreq ? { changefreq } : {},
      ...priority ? { priority } : {}
    }] : [],
    issues
  };
}
function imageEntries(node) {
  return many(node, "image").flatMap((image) => {
    const loc = text(child(image, "loc"));
    if (!loc)
      return [];
    const caption = text(child(image, "caption"));
    const geoLocation = text(child(image, "geo_location"));
    const title = text(child(image, "title"));
    const license = text(child(image, "license"));
    return [{
      loc,
      ...caption ? { caption } : {},
      ...geoLocation ? { geoLocation } : {},
      ...title ? { title } : {},
      ...license ? { license } : {}
    }];
  });
}
function alternatives(node) {
  return many(node, "link").flatMap((link) => {
    const href = attribute(link, "href");
    const hreflang = attribute(link, "hreflang");
    if (!href || !hreflang)
      return [];
    const rel = attribute(link, "rel");
    return [{ href, hreflang, ...rel ? { rel } : {} }];
  });
}
function media(node) {
  const contents = many(node, "content").flatMap((content) => {
    const url = attribute(content, "url");
    if (!url)
      return [];
    const type = attribute(content, "type");
    const medium = attribute(content, "medium");
    return [{ url, ...type ? { type } : {}, ...medium ? { medium } : {} }];
  });
  const thumbnails = many(node, "thumbnail").flatMap((thumbnail) => {
    const url = attribute(thumbnail, "url");
    if (!url)
      return [];
    const width = attribute(thumbnail, "width");
    const height = attribute(thumbnail, "height");
    return [{ url, ...width ? { width } : {}, ...height ? { height } : {} }];
  });
  if (contents.length === 0 && thumbnails.length === 0)
    return void 0;
  return {
    ...contents.length > 0 ? { contents } : {},
    ...thumbnails.length > 0 ? { thumbnails } : {}
  };
}
function localizeRecord(value) {
  if (Array.isArray(value))
    return value.map(localizeRecord);
  if (!value || typeof value !== "object")
    return value;
  return Object.fromEntries(
    Object.entries(value).map(([key, childValue]) => [
      localName(key),
      localizeRecord(childValue)
    ])
  );
}
function extensions(node) {
  if (!node || typeof node !== "object")
    return void 0;
  let hasExtension = false;
  for (const key in node) {
    const name = localName(key);
    if (name === "image" || name === "link" || name === "content" || name === "thumbnail" || name === "video" || name === "news") {
      hasExtension = true;
      break;
    }
  }
  if (!hasExtension)
    return void 0;
  const images = imageEntries(node);
  const alternateEntries = alternatives(node);
  const mediaEntries = media(node);
  const videos = many(node, "video").filter((value) => value && typeof value === "object").map((value) => localizeRecord(value));
  const news = child(node, "news");
  if (images.length === 0 && alternateEntries.length === 0 && !mediaEntries && videos.length === 0 && !news)
    return void 0;
  return {
    ...images.length > 0 ? { images } : {},
    ...alternateEntries.length > 0 ? { alternatives: alternateEntries } : {},
    ...videos.length > 0 ? { videos } : {},
    ...news && typeof news === "object" ? { news: localizeRecord(news) } : {},
    ...mediaEntries ? { media: mediaEntries } : {}
  };
}
function urlRecord(node, loc) {
  const lastmod = text(child(node, "lastmod"));
  const changefreq = text(child(node, "changefreq"));
  const priority = text(child(node, "priority"));
  const parsedExtensions = extensions(node);
  return {
    loc,
    ...lastmod ? { lastmod } : {},
    ...changefreq ? { changefreq } : {},
    ...priority ? { priority } : {},
    ...parsedExtensions ? { extensions: parsedExtensions } : {}
  };
}
function parseUrlset(root) {
  const issues = [];
  const entries = [];
  for (const [index, node] of many(root, "url").entries()) {
    const loc = text(child(node, "loc"));
    const locIssue = issueForLoc(loc, index);
    if (locIssue)
      issues.push(locIssue);
    if (loc)
      entries.push(urlRecord(node, loc));
  }
  return { _tag: "urlset", format: "xml", entries, issues };
}
function parseIndex(root) {
  const issues = [];
  const entries = [];
  for (const [index, node] of many(root, "sitemap").entries()) {
    const loc = text(child(node, "loc"));
    const locIssue = issueForLoc(loc, index);
    if (locIssue)
      issues.push(locIssue);
    if (!loc)
      continue;
    const lastmod = text(child(node, "lastmod"));
    entries.push({ loc, ...lastmod ? { lastmod } : {} });
  }
  return { _tag: "index", format: "xml", entries, issues };
}
function parseRss(root) {
  const issues = [];
  const entries = [];
  const channel = child(root, "channel");
  for (const [index, item] of many(channel, "item").entries()) {
    const loc = text(child(item, "link"));
    const locIssue = issueForLoc(loc, index);
    if (locIssue)
      issues.push(locIssue);
    if (!loc)
      continue;
    const lastmod = text(child(item, "pubDate"));
    const parsedMedia = media(item);
    entries.push({
      loc,
      ...lastmod ? { lastmod } : {},
      ...parsedMedia ? { extensions: { media: parsedMedia } } : {}
    });
  }
  return { _tag: "urlset", format: "rss2", entries, issues };
}
function parseAtom(root) {
  const issues = [];
  const entries = [];
  for (const [index, entry] of many(root, "entry").entries()) {
    const links = many(entry, "link");
    const alternate = links.find((link) => !attribute(link, "rel") || attribute(link, "rel") === "alternate");
    const loc = alternate ? attribute(alternate, "href") : void 0;
    const locIssue = issueForLoc(loc, index);
    if (locIssue)
      issues.push(locIssue);
    if (!loc)
      continue;
    const lastmod = text(child(entry, "updated")) ?? text(child(entry, "published"));
    const parsedMedia = media(entry);
    entries.push({
      loc,
      ...lastmod ? { lastmod } : {},
      ...parsedMedia ? { extensions: { media: parsedMedia } } : {}
    });
  }
  return { _tag: "urlset", format: "atom1", entries, issues };
}
function parseDocument(xml) {
  const validation = XMLValidator.validate(xml);
  if (validation !== true)
    return { _tag: "malformed", detail: validation.err.msg };
  try {
    return { _tag: "document", document: parser.parse(xml) };
  } catch (error) {
    return {
      _tag: "malformed",
      detail: error instanceof Error ? error.message : String(error)
    };
  }
}
function parseXmlRecord(xml, recordTag) {
  const simple = parseSimpleRecord(xml, recordTag);
  if (simple)
    return simple;
  const parsed = parseDocument(xml);
  if (parsed._tag === "malformed")
    return parsed;
  const rootEntry = Object.entries(parsed.document).find(([name]) => !name.startsWith("?"));
  if (!rootEntry || localName(rootEntry[0]).toLowerCase() !== recordTag) {
    return recordTag === "sitemap" ? { _tag: "index", format: "xml", entries: [], issues: [] } : {
      _tag: "urlset",
      format: recordTag === "item" ? "rss2" : recordTag === "entry" ? "atom1" : "xml",
      entries: [],
      issues: []
    };
  }
  const root = rootEntry[1];
  switch (recordTag) {
    case "url":
      return parseUrlset({ url: root });
    case "sitemap":
      return parseIndex({ sitemap: root });
    case "item":
      return parseRss({ channel: { item: root } });
    case "entry":
      return parseAtom({ entry: root });
  }
}

const DEFAULT_MAX_DECODED_BYTES = 50 * 1024 * 1024;
const DEFAULT_MAX_ENTRIES = 5e4;
const DEFAULT_MAX_ENTRY_BYTES = 1024 * 1024;
const RECORD_OPEN_PATTERNS = {
  url: /^<((?:[\w.-]+:)?url)\b/i,
  sitemap: /^<((?:[\w.-]+:)?sitemap)\b/i,
  item: /^<((?:[\w.-]+:)?item)\b/i,
  entry: /^<((?:[\w.-]+:)?entry)\b/i
};
function parseLimit(value, fallback, name) {
  if (value === void 0)
    return fallback;
  if (!Number.isFinite(value) || value < 0 || !Number.isInteger(value))
    throw new RangeError(`${name} must be a non-negative finite integer`);
  return value;
}
function issue(code, message, severity = "error") {
  return { code, severity, message };
}
function summary(stats, entriesRead) {
  return {
    bytesRead: stats.bytesRead,
    entriesRead,
    compressed: stats.compressed
  };
}
function findMarkupEnd(input, start) {
  let quote = "";
  for (let index = start + 1; index < input.length; index++) {
    const character = input[index];
    if (quote) {
      if (character === quote)
        quote = "";
      continue;
    }
    if (character === '"' || character === "'") {
      quote = character;
      continue;
    }
    if (character === ">")
      return index;
  }
  return -1;
}
function isXmlWhitespace(character) {
  return character === " " || character === "	" || character === "\n" || character === "\r";
}
function isSelfClosingMarkup(markup) {
  let cursor = markup.length - 2;
  while (cursor >= 0 && isXmlWhitespace(markup[cursor]))
    cursor--;
  return markup[cursor] === "/";
}
function trimMarkupPrefix(input) {
  let output = input.trimStart();
  while (true) {
    if (output.startsWith("<?")) {
      const end = output.indexOf("?>");
      if (end === -1)
        return output;
      output = output.slice(end + 2).trimStart();
      continue;
    }
    if (output.startsWith("<!--")) {
      const end = output.indexOf("-->");
      if (end === -1)
        return output;
      output = output.slice(end + 3).trimStart();
      continue;
    }
    return output;
  }
}
function detectRoot(input) {
  const source = trimMarkupPrefix(input);
  if (source.startsWith("<!--") || source.startsWith("<?"))
    return void 0;
  if (!source.startsWith("<"))
    return void 0;
  if (/^<!doctype\b/i.test(source) || /^<html\b/i.test(source)) {
    return {
      _tag: "malformed",
      detail: /^<html\b|^<!DOCTYPE\s+html\b/i.test(source) ? "html" : "Document type declarations are not supported"
    };
  }
  const end = findMarkupEnd(source, 0);
  if (end === -1)
    return void 0;
  const openTag = source.slice(0, end + 1);
  const match = /^<([A-Z_][\w.:-]*)\b/i.exec(openTag);
  const qualifiedName = match?.[1];
  const name = qualifiedName?.split(":").at(-1)?.toLowerCase();
  if (name === "urlset") {
    return {
      name,
      qualifiedName,
      format: "xml",
      kind: "urlset",
      openTag,
      recordTag: "url",
      containerReady: true
    };
  }
  if (name === "sitemapindex") {
    return {
      name,
      qualifiedName,
      format: "xml",
      kind: "index",
      openTag,
      recordTag: "sitemap",
      containerReady: true
    };
  }
  if (name === "rss") {
    return {
      name,
      qualifiedName,
      format: "rss2",
      kind: "urlset",
      openTag,
      recordTag: "item",
      containerReady: false
    };
  }
  if (name === "feed") {
    return {
      name,
      qualifiedName,
      format: "atom1",
      kind: "urlset",
      openTag,
      recordTag: "entry",
      containerReady: true
    };
  }
  return { _tag: "malformed", detail: "unsupported" };
}
function afterRootOpen(input, root) {
  const source = trimMarkupPrefix(input);
  return source.slice(root.openTag.length);
}
function prepareRssContainer(input) {
  const source = trimMarkupPrefix(input);
  if (!source.startsWith("<"))
    return void 0;
  const end = findMarkupEnd(source, 0);
  if (end === -1)
    return void 0;
  if (!/^<channel\b/i.test(source.slice(0, end + 1)))
    return { _tag: "malformed", detail: "RSS document is missing its channel element" };
  return { ready: true, rest: source.slice(end + 1) };
}
function extractFeedMetadata(source, maxEntryBytes) {
  if (!source.startsWith("<"))
    return { _tag: "malformed", detail: "Unexpected text inside feed" };
  const openingEnd = findMarkupEnd(source, 0);
  if (openingEnd === -1)
    return void 0;
  const opening = /^<([A-Z_][\w.:-]*)\b/i.exec(source);
  if (!opening)
    return { _tag: "malformed", detail: "Unexpected markup inside feed" };
  if (/\/\s*>$/.test(source.slice(0, openingEnd + 1)))
    return { _tag: "skip", rest: source.slice(openingEnd + 1) };
  const stack = [opening[1].toLowerCase()];
  let cursor = openingEnd + 1;
  while (cursor < source.length) {
    const markupStart = source.indexOf("<", cursor);
    if (markupStart === -1)
      break;
    if (source.startsWith("<!--", markupStart)) {
      const end = source.indexOf("-->", markupStart + 4);
      if (end === -1)
        return void 0;
      cursor = end + 3;
      continue;
    }
    if (source.startsWith("<![CDATA[", markupStart)) {
      const end = source.indexOf("]]>", markupStart + 9);
      if (end === -1)
        return void 0;
      cursor = end + 3;
      continue;
    }
    if (source.startsWith("<?", markupStart)) {
      const end = source.indexOf("?>", markupStart + 2);
      if (end === -1)
        return void 0;
      cursor = end + 2;
      continue;
    }
    const markupEnd = findMarkupEnd(source, markupStart);
    if (markupEnd === -1)
      return void 0;
    const markup = source.slice(markupStart, markupEnd + 1);
    const tag = /^<(\/?)[ \t\r\n]*([A-Z_][\w.:-]*)\b/i.exec(markup);
    if (!tag)
      return { _tag: "malformed", detail: "Unexpected markup inside feed metadata" };
    const name = tag[2].toLowerCase();
    if (tag[1]) {
      const expected = stack.pop();
      if (expected !== name)
        return { _tag: "malformed", detail: `Mismatched closing element in feed metadata: ${tag[2]}` };
      if (stack.length === 0)
        return { _tag: "skip", rest: source.slice(markupEnd + 1) };
    } else if (!/\/\s*>$/.test(markup)) {
      stack.push(name);
    }
    cursor = markupEnd + 1;
  }
  if (new TextEncoder().encode(source).byteLength > maxEntryBytes)
    return { _tag: "malformed", detail: `Sitemap metadata element exceeds ${maxEntryBytes} bytes` };
  return void 0;
}
function startsWithCI(input, prefix) {
  return input.length >= prefix.length && input.slice(0, prefix.length).toLowerCase() === prefix.toLowerCase();
}
function extractRecord(input, root, maxEntryBytes) {
  const source = trimMarkupPrefix(input);
  if (source.startsWith("<!--") || source.startsWith("<?"))
    return void 0;
  const rootClose = `</${root.qualifiedName}>`;
  if (startsWithCI(source, rootClose))
    return { _tag: "close", rest: source.slice(rootClose.length) };
  if (root.name === "rss" && startsWithCI(source, "</channel>")) {
    const rest = trimMarkupPrefix(source.slice("</channel>".length));
    const rssClose = `</${root.qualifiedName}>`;
    if (startsWithCI(rest, rssClose))
      return { _tag: "close", rest: rest.slice(rssClose.length) };
    if (rest.length > 0 && findMarkupEnd(rest, 0) !== -1)
      return { _tag: "malformed", detail: "RSS channel is not followed by its closing root" };
    return void 0;
  }
  const directOpen = `<${root.recordTag}`;
  const directBoundary = source[directOpen.length];
  const directName = source.startsWith(directOpen) && (directBoundary === ">" || directBoundary === "/" || isXmlWhitespace(directBoundary)) ? root.recordTag : void 0;
  const qualifiedName = directName ?? RECORD_OPEN_PATTERNS[root.recordTag].exec(source)?.[1];
  if (!qualifiedName) {
    if (source.length === 0)
      return void 0;
    if (root.name === "rss" || root.name === "feed")
      return extractFeedMetadata(source, maxEntryBytes);
    if (findMarkupEnd(source, 0) !== -1)
      return { _tag: "malformed", detail: `Unexpected element inside ${root.name}` };
    return void 0;
  }
  const openingEnd = findMarkupEnd(source, 0);
  if (openingEnd === -1)
    return void 0;
  if (isSelfClosingMarkup(source.slice(0, openingEnd + 1))) {
    return {
      _tag: "record",
      record: source.slice(0, openingEnd + 1),
      rest: source.slice(openingEnd + 1)
    };
  }
  const close = `</${qualifiedName}>`;
  const closeIndex = findRecordClose(source, close, openingEnd + 1);
  if (closeIndex === -1) {
    if (new TextEncoder().encode(source).byteLength > maxEntryBytes) {
      return {
        _tag: "malformed",
        detail: `Sitemap entry exceeds ${maxEntryBytes} bytes`
      };
    }
    return void 0;
  }
  const end = closeIndex + close.length;
  return {
    _tag: "record",
    record: source.slice(0, end),
    rest: source.slice(end)
  };
}
function escapeRegExp(value) {
  return value.replace(/[.*+?^${}()|[\]\\]/g, "\\$&");
}
function findRecordClose(input, close, start) {
  let closePattern;
  let cursor = start;
  while (true) {
    let closeIndex = input.indexOf(close, cursor);
    if (closeIndex === -1) {
      closePattern ||= new RegExp(escapeRegExp(close), "gi");
      closePattern.lastIndex = cursor;
      const match = closePattern.exec(input);
      if (!match)
        return -1;
      closeIndex = match.index;
    }
    const window = input.slice(cursor, closeIndex);
    const commentIndexRel = window.indexOf("<!--");
    const cdataIndexRel = window.indexOf("<![CDATA[");
    const hiddenIndexRel = commentIndexRel === -1 ? cdataIndexRel : cdataIndexRel === -1 ? commentIndexRel : Math.min(commentIndexRel, cdataIndexRel);
    if (hiddenIndexRel === -1)
      return closeIndex;
    const marker = hiddenIndexRel === commentIndexRel ? "-->" : "]]>";
    const hiddenEnd = input.indexOf(marker, cursor + hiddenIndexRel);
    if (hiddenEnd === -1)
      return -1;
    cursor = hiddenEnd + marker.length;
  }
}
function parseRecord(root, record) {
  const parsed = parseXmlRecord(record, root.recordTag);
  if (parsed._tag === "malformed")
    return { issues: [], malformed: parsed.detail };
  if (parsed._tag === "unsupported")
    return { issues: [], malformed: "Unsupported sitemap entry" };
  const entry = parsed.entries[0];
  return {
    ...entry ? { entry } : {},
    issues: parsed.issues
  };
}
function textEntry(line, index) {
  const loc = line.trim();
  if (!loc)
    return {};
  let valid = false;
  try {
    const url = new URL(loc);
    valid = url.protocol === "http:" || url.protocol === "https:";
  } catch {
    valid = false;
  }
  return {
    entry: { loc },
    ...!valid ? {
      issue: {
        code: "invalid_loc",
        severity: "warning",
        message: "Text sitemap entry is not an absolute HTTP(S) URL",
        entryIndex: index,
        field: "loc",
        value: loc
      }
    } : {}
  };
}
async function* parseSitemap(input, options = {}) {
  const maxDecodedBytes = parseLimit(
    options.maxDecodedBytes,
    DEFAULT_MAX_DECODED_BYTES,
    "maxDecodedBytes"
  );
  const maxEntries = parseLimit(options.maxEntries, DEFAULT_MAX_ENTRIES, "maxEntries");
  const maxEntryBytes = parseLimit(
    options.maxEntryBytes,
    DEFAULT_MAX_ENTRY_BYTES,
    "maxEntryBytes"
  );
  const stats = { bytesRead: 0, compressed: false };
  const chunks = decodedTextChunks(input, maxDecodedBytes, stats);
  let entriesRead = 0;
  let buffer = "";
  let root;
  let closed = false;
  let sawText = false;
  try {
    for await (const chunk of chunks) {
      buffer += chunk;
      sawText ||= chunk.trim().length > 0;
      if (options.formatHint === "text") {
        while (true) {
          const newline = buffer.indexOf("\n");
          if (newline === -1)
            break;
          const line = buffer.slice(0, newline).replace(/\r$/, "");
          buffer = buffer.slice(newline + 1);
          const parsed = textEntry(line, entriesRead);
          if (!parsed.entry)
            continue;
          if (entriesRead >= maxEntries) {
            const completeness = { _tag: "partial", reason: "entry_limit" };
            yield { _tag: "issue", issue: issue("entry_limit", `Sitemap exceeds ${maxEntries} entries`) };
            yield { _tag: "end", completeness, summary: summary(stats, entriesRead) };
            return;
          }
          if (entriesRead === 0)
            yield { _tag: "document", format: "text", kind: "urlset" };
          yield { _tag: "url", entry: parsed.entry };
          if (parsed.issue)
            yield { _tag: "issue", issue: parsed.issue };
          entriesRead++;
        }
        continue;
      }
      if (!root) {
        const detected = detectRoot(buffer);
        if (!detected)
          continue;
        if ("_tag" in detected) {
          const reason = detected.detail === "html" ? "html" : detected.detail === "unsupported" ? "unsupported" : "malformed";
          yield { _tag: "issue", issue: issue(reason, detected.detail) };
          yield {
            _tag: "end",
            completeness: { _tag: "failed", reason },
            summary: summary(stats, entriesRead)
          };
          return;
        }
        root = detected;
        buffer = afterRootOpen(buffer, root);
        yield { _tag: "document", format: root.format, kind: root.kind };
        if (isSelfClosingMarkup(root.openTag)) {
          closed = true;
          continue;
        }
      }
      if (closed)
        continue;
      if (!root.containerReady) {
        const container = prepareRssContainer(buffer);
        if (!container)
          continue;
        if ("_tag" in container) {
          yield { _tag: "issue", issue: issue("malformed", container.detail) };
          yield {
            _tag: "end",
            completeness: { _tag: "failed", reason: "malformed" },
            summary: summary(stats, entriesRead)
          };
          return;
        }
        root.containerReady = true;
        buffer = container.rest;
      }
      while (true) {
        const extracted = extractRecord(buffer, root, maxEntryBytes);
        if (!extracted)
          break;
        if (extracted._tag === "malformed") {
          yield { _tag: "issue", issue: issue("malformed", extracted.detail) };
          yield {
            _tag: "end",
            completeness: { _tag: "failed", reason: "malformed" },
            summary: summary(stats, entriesRead)
          };
          return;
        }
        if (extracted._tag === "close") {
          buffer = extracted.rest;
          closed = true;
          break;
        }
        if (extracted._tag === "skip") {
          buffer = extracted.rest;
          continue;
        }
        if (entriesRead >= maxEntries) {
          const completeness = { _tag: "partial", reason: "entry_limit" };
          yield { _tag: "issue", issue: issue("entry_limit", `Sitemap exceeds ${maxEntries} entries`) };
          yield { _tag: "end", completeness, summary: summary(stats, entriesRead) };
          return;
        }
        const parsed = parseRecord(root, extracted.record);
        if (parsed.malformed) {
          yield { _tag: "issue", issue: issue("malformed", parsed.malformed) };
          yield {
            _tag: "end",
            completeness: { _tag: "failed", reason: "malformed" },
            summary: summary(stats, entriesRead)
          };
          return;
        }
        for (const parsedIssue of parsed.issues)
          yield { _tag: "issue", issue: parsedIssue };
        if (parsed.entry) {
          if (root.kind === "urlset")
            yield { _tag: "url", entry: parsed.entry };
          else
            yield { _tag: "sitemap", entry: parsed.entry };
          entriesRead++;
        }
        buffer = extracted.rest;
      }
    }
    if (options.formatHint === "text") {
      const parsed = textEntry(buffer.replace(/\r$/, ""), entriesRead);
      if (parsed.entry) {
        if (entriesRead >= maxEntries) {
          yield { _tag: "issue", issue: issue("entry_limit", `Sitemap exceeds ${maxEntries} entries`) };
          yield {
            _tag: "end",
            completeness: { _tag: "partial", reason: "entry_limit" },
            summary: summary(stats, entriesRead)
          };
          return;
        }
        if (entriesRead === 0)
          yield { _tag: "document", format: "text", kind: "urlset" };
        yield { _tag: "url", entry: parsed.entry };
        if (parsed.issue)
          yield { _tag: "issue", issue: parsed.issue };
        entriesRead++;
      }
      if (entriesRead === 0 && !sawText) {
        yield { _tag: "issue", issue: issue("empty", "Sitemap body is empty") };
        yield {
          _tag: "end",
          completeness: { _tag: "failed", reason: "empty" },
          summary: summary(stats, entriesRead)
        };
        return;
      }
      yield {
        _tag: "end",
        completeness: { _tag: "complete" },
        summary: summary(stats, entriesRead)
      };
      return;
    }
    if (!root) {
      const reason = sawText ? "unsupported" : "empty";
      yield {
        _tag: "issue",
        issue: issue(reason, reason === "empty" ? "Sitemap body is empty" : "Document is not a supported sitemap format")
      };
      yield {
        _tag: "end",
        completeness: { _tag: "failed", reason },
        summary: summary(stats, entriesRead)
      };
      return;
    }
    if (!closed || trimMarkupPrefix(buffer).length > 0) {
      yield { _tag: "issue", issue: issue("malformed", `Unclosed or trailing content in ${root.name}`) };
      yield {
        _tag: "end",
        completeness: { _tag: "failed", reason: "malformed" },
        summary: summary(stats, entriesRead)
      };
      return;
    }
    yield {
      _tag: "end",
      completeness: { _tag: "complete" },
      summary: summary(stats, entriesRead)
    };
  } catch (error) {
    if (!isSitemapInputFailure(error))
      throw error;
    yield { _tag: "issue", issue: issue(error.reason, error.message) };
    const completeness = error.reason === "decoded_limit" ? { _tag: "partial", reason: "decoded_limit" } : { _tag: "failed", reason: error.reason };
    yield { _tag: "end", completeness, summary: summary(stats, entriesRead) };
  }
}
async function collectSitemap(input, options = {}) {
  let document;
  const issues = [];
  let end;
  for await (const event of parseSitemap(input, options)) {
    if (event._tag === "document") {
      document = event.kind === "urlset" ? { _tag: "urlset", format: event.format, entries: [] } : { _tag: "index", format: "xml", entries: [] };
    } else if (event._tag === "url" && document?._tag === "urlset") {
      document.entries.push(event.entry);
    } else if (event._tag === "sitemap" && document?._tag === "index") {
      document.entries.push(event.entry);
    } else if (event._tag === "issue") {
      issues.push(event.issue);
    } else if (event._tag === "end") {
      end = event;
    }
  }
  if (!end)
    throw new Error("Sitemap parser ended without a terminal event");
  if (end.completeness._tag === "failed") {
    return {
      _tag: "failure",
      issues,
      completeness: end.completeness,
      summary: end.summary
    };
  }
  if (!document) {
    return {
      _tag: "partial",
      issues,
      completeness: end.completeness,
      summary: end.summary
    };
  }
  return {
    _tag: "document",
    document,
    issues,
    completeness: end.completeness,
    summary: end.summary
  };
}

export { collectSitemap, parseSitemap };
