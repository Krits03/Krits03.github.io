import { createPathFilter, resolveI18nRouteEntries, splitForLocales } from "../../../utils-pure.js";
import { preNormalizeEntry } from "../urlset/normalise.js";
export function resolveSitemapEntries(sitemap, urls, runtimeConfig, resolvers, baseURL) {
  const {
    autoI18n,
    isI18nMapped
  } = runtimeConfig;
  const hasFilters = !!sitemap.include?.length || !!sitemap.exclude?.length;
  const filterPath = hasFilters ? createPathFilter({
    include: sitemap.include,
    exclude: sitemap.exclude
  }, baseURL || "/") : void 0;
  const _urls = [];
  for (const _e of urls) {
    const e = preNormalizeEntry(_e, resolvers);
    if (e.loc && (!filterPath || filterPath(e.loc, e._path?.pathname)))
      _urls.push(e);
  }
  const withoutPrefixPaths = {};
  if (autoI18n && autoI18n.strategy !== "no_prefix") {
    const localeCodes = new Set(autoI18n.locales.map((l) => l.code));
    const localeByCode = new Map(autoI18n.locales.map((l) => [l.code, l]));
    const defaultLocale = autoI18n.defaultLocale;
    const hasDifferentDomains = !!autoI18n.differentDomains;
    const validI18nUrlsForTransform = [];
    for (let i = 0; i < _urls.length; i++) {
      const _e = _urls[i];
      if (_e._abs)
        continue;
      const split = splitForLocales(_e._relativeLoc, localeCodes);
      let localeCode = split[0];
      const pathWithoutPrefix = split[1];
      if (!localeCode)
        localeCode = defaultLocale;
      const e = _e;
      e._pathWithoutPrefix = pathWithoutPrefix;
      const locale = localeByCode.get(localeCode);
      if (!locale)
        continue;
      e._locale = locale;
      e._index = i;
      e._key = `${e._sitemap || ""}${e._path?.pathname || "/"}${e._path?.search || ""}`;
      withoutPrefixPaths[pathWithoutPrefix] = withoutPrefixPaths[pathWithoutPrefix] || [];
      if (!withoutPrefixPaths[pathWithoutPrefix].some((e2) => e2._locale.code === locale.code))
        withoutPrefixPaths[pathWithoutPrefix].push(e);
      validI18nUrlsForTransform.push(e);
    }
    for (const e of validI18nUrlsForTransform) {
      if (!e._i18nTransform && !e.alternatives?.length) {
        const alternatives = [];
        for (const u of withoutPrefixPaths[e._pathWithoutPrefix] || []) {
          if (u._locale.code === defaultLocale) {
            alternatives.push({
              href: u.loc,
              hreflang: "x-default"
            });
          }
          alternatives.push({
            href: u.loc,
            hreflang: u._locale._hreflang || defaultLocale
          });
        }
        if (alternatives.length)
          e.alternatives = alternatives;
      } else if (e._i18nTransform) {
        delete e._i18nTransform;
        const routeEntries = resolveI18nRouteEntries(e._relativeLoc, autoI18n, (href) => !filterPath || filterPath(href));
        if (hasDifferentDomains) {
          e.alternatives = routeEntries[0]?.alternatives;
        } else {
          for (const { alternatives, locale: l, loc } of routeEntries) {
            const _sitemap = isI18nMapped ? l._sitemap : void 0;
            const { _index: _, ...rest } = e;
            const newEntry = preNormalizeEntry({
              _sitemap,
              ...rest,
              _key: `${_sitemap || ""}${loc || "/"}`,
              _locale: l,
              loc,
              alternatives
            }, resolvers);
            if (e._locale.code === newEntry._locale.code) {
              _urls[e._index] = newEntry;
              e._index = void 0;
            } else {
              _urls.push(newEntry);
            }
          }
        }
      }
      if (isI18nMapped) {
        e._sitemap = e._sitemap || e._locale._sitemap;
        e._key = `${e._sitemap || ""}${e.loc || "/"}${e._path?.search || ""}`;
      }
      if (e._index)
        _urls[e._index] = e;
    }
  }
  return _urls;
}
