import { createConsola } from 'consola';
import { toRouteMatcher, createRouter } from 'radix3';

function parseSerializedRegExp(value) {
  const lastSlash = value.lastIndexOf("/");
  return new RegExp(value.slice(1, lastSlash), value.slice(lastSlash + 1));
}
function serializeFilters(filters, tag) {
  const prefix = tag ? `[${tag}] ` : "";
  const result = [];
  for (const filter of filters) {
    if (filter instanceof RegExp) {
      result.push({ regex: filter.toString() });
      continue;
    }
    if (typeof filter === "string") {
      result.push(filter);
      continue;
    }
    if (filter && typeof filter === "object" && typeof filter.regex === "string") {
      result.push(filter);
      continue;
    }
    if (filter && typeof filter === "object" && typeof filter.source === "string") {
      result.push(filter);
      continue;
    }
    console.warn(`${prefix}You have provided an invalid filter: ${filter}, ignoring.`);
  }
  return result;
}
function deserializeFilters(filters) {
  return filters.map((filter) => {
    if (filter instanceof RegExp || typeof filter === "string")
      return filter;
    if (typeof filter.regex === "string")
      return parseSerializedRegExp(filter.regex);
    if (typeof filter.source === "string")
      return new RegExp(filter.source, filter.flags || "");
    return filter;
  });
}
function createFilter(options = {}) {
  const include = deserializeFilters(options.include || []);
  const exclude = deserializeFilters(options.exclude || []);
  if (include.length === 0 && exclude.length === 0)
    return () => true;
  const excludeRegex = exclude.filter((r) => r instanceof RegExp);
  const includeRegex = include.filter((r) => r instanceof RegExp);
  const excludeStrings = exclude.filter((r) => typeof r === "string");
  const includeStrings = include.filter((r) => typeof r === "string");
  const excludeMatcher = excludeStrings.length > 0 ? toRouteMatcher(createRouter({
    routes: Object.fromEntries(excludeStrings.map((r) => [r, true])),
    strictTrailingSlash: false
  })) : null;
  const includeMatcher = includeStrings.length > 0 ? toRouteMatcher(createRouter({
    routes: Object.fromEntries(includeStrings.map((r) => [r, true])),
    strictTrailingSlash: false
  })) : null;
  const excludeExact = new Set(excludeStrings);
  const includeExact = new Set(includeStrings);
  return function(path) {
    if (excludeRegex.some((r) => r.test(path)))
      return false;
    if (excludeExact.has(path))
      return false;
    if (excludeMatcher && excludeMatcher.matchAll(path).length > 0)
      return false;
    if (includeRegex.some((r) => r.test(path)))
      return true;
    if (includeExact.has(path))
      return true;
    if (includeMatcher && includeMatcher.matchAll(path).length > 0)
      return true;
    return include.length === 0;
  };
}
function withoutQuery(path) {
  return path.split("?")[0];
}
function createModuleLogger(tag, debug) {
  return createConsola({ level: debug ? 4 : 3, defaults: { tag } });
}

export { createFilter, createModuleLogger, deserializeFilters, serializeFilters, withoutQuery };
