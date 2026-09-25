import { createDefu } from "defu";
import { computeLocaleAlternates, resolveLocaleFromRoute } from "nuxtseo-shared/i18n-runtime";
import { createFilter, createModuleLogger } from "nuxtseo-shared/utils";
import { joinURL, parseURL, withHttps, withLeadingSlash, withoutBase } from "ufo";
export { createFilter } from "nuxtseo-shared/utils";
export const logger = createModuleLogger("@nuxt/sitemap");
const XML_ENTITIES = {
  "&": "&amp;",
  "<": "&lt;",
  ">": "&gt;",
  '"': "&quot;",
  "'": "&apos;"
};
const XML_SPECIAL_CHARS_RE = /[&<>"']/g;
const HAS_XML_SPECIAL_CHARS_RE = /[&<>"']/;
export function xmlEscape(value) {
  const input = String(value);
  return HAS_XML_SPECIAL_CHARS_RE.test(input) ? input.replace(XML_SPECIAL_CHARS_RE, (char) => XML_ENTITIES[char]) : input;
}
const merger = createDefu((obj, key, value) => {
  if (Array.isArray(obj[key]) && Array.isArray(value))
    obj[key] = Array.from(/* @__PURE__ */ new Set([...obj[key], ...value]));
  return obj[key];
});
export function mergeOnKey(arr, key, onMerge) {
  if (arr.length < 2)
    return arr;
  const seen = /* @__PURE__ */ new Map();
  let resultLength = 0;
  for (const item of arr) {
    const k = item[key];
    if (seen.has(k)) {
      const existingIndex = seen.get(k);
      onMerge?.(item[key]);
      arr[existingIndex] = merger(item, arr[existingIndex]);
    } else {
      seen.set(k, resultLength);
      arr[resultLength++] = item;
    }
  }
  arr.length = resultLength;
  return arr;
}
export function splitForLocales(path, locales) {
  const start = path.charCodeAt(0) === 47 ? 1 : 0;
  const end = path.indexOf("/", start);
  const prefix = path.slice(start, end === -1 ? path.length : end);
  const hasLocale = locales instanceof Set ? locales.has(prefix) : locales.includes(prefix);
  if (prefix && hasLocale) {
    const prefixEnd = start + prefix.length;
    return [prefix, start === 1 ? path.slice(prefixEnd) : path];
  }
  return [null, path];
}
function toRuntimeI18nConfig(i18n) {
  return {
    ...i18n,
    // Sitemap transforms keep the unprefixed default URL alongside Nuxt's prefixed route.
    strategy: i18n.strategy === "prefix_and_default" ? "prefix_except_default" : i18n.strategy,
    pages: i18n.pages && Object.fromEntries(
      Object.entries(i18n.pages).map(([pageName, pageLocales]) => [
        pageName,
        Object.fromEntries(i18n.locales.map((locale) => {
          const configuredPath = pageLocales[locale.code];
          return [locale.code, configuredPath === void 0 ? withLeadingSlash(pageName) : configuredPath];
        }))
      ])
    ),
    locales: i18n.locales.map((locale) => ({
      ...locale,
      hreflang: locale._hreflang
    }))
  };
}
function localeAlternateHref(alternate) {
  return alternate.domain ? joinURL(withHttps(alternate.domain), alternate.path) : alternate.path;
}
export function resolveI18nRouteEntries(route, i18n, includeHref = () => true) {
  const runtimeConfig = toRuntimeI18nConfig(i18n);
  const currentLocale = resolveLocaleFromRoute(route, runtimeConfig).locale;
  const alternates = computeLocaleAlternates(route, runtimeConfig, { locale: currentLocale });
  const localizedAlternates = alternates.map((alternate) => ({
    alternate,
    href: localeAlternateHref(alternate)
  }));
  const defaultHref = localizedAlternates.find(({ alternate }) => alternate.code === i18n.defaultLocale)?.href;
  const sitemapAlternatives = [
    ...defaultHref && includeHref(defaultHref) ? [{ hreflang: "x-default", href: defaultHref }] : [],
    ...localizedAlternates.filter(({ href }) => includeHref(href)).map(({ alternate, href }) => ({ hreflang: alternate.hreflang, href }))
  ];
  return localizedAlternates.flatMap(({ alternate, href }) => {
    const locale = i18n.locales.find((locale2) => locale2.code === alternate.code);
    return locale ? [{ locale, loc: href, alternatives: sitemapAlternatives }] : [];
  });
}
export function resolveI18nSitemapLocaleKey(sitemapName, localeSitemapKeys) {
  let best = null;
  for (const key of localeSitemapKeys) {
    if (sitemapName === key || sitemapName.startsWith(`${key}-`)) {
      if (best === null || key.length > best.length)
        best = key;
    }
  }
  return best;
}
const StringifiedRegExpPattern = /\/(.*?)\/([gimsuy]*)$/;
export function normalizeRuntimeFilters(input) {
  return (input || []).map((rule) => {
    if (rule instanceof RegExp || typeof rule === "string")
      return rule;
    const match = rule.regex.match(StringifiedRegExpPattern);
    if (match)
      return new RegExp(match[1], match[2]);
    return false;
  }).filter(Boolean);
}
export function createPathFilter(options = {}, baseURL) {
  const urlFilter = createFilter({
    include: normalizeRuntimeFilters(options.include),
    exclude: normalizeRuntimeFilters(options.exclude)
  });
  const hasBase = baseURL && baseURL !== "/";
  return (loc, pathname) => {
    let path = pathname;
    if (typeof path !== "string") {
      try {
        path = parseURL(loc).pathname;
      } catch {
        return false;
      }
    }
    if (hasBase)
      path = withoutBase(path, baseURL);
    return urlFilter(withLeadingSlash(path));
  };
}
