import { getNuxtModuleVersion, hasNuxtModuleCompatibility, hasNuxtModule } from '@nuxt/kit';
import { withHttps, withBase } from 'ufo';
import { localePath, resolveLocaleAlternates, resolveLocaleFromRoute } from './i18n-runtime.mjs';
import { getNuxtModuleOptions } from './kit.mjs';
import 'node:url';
import 'pathe';
import 'pkg-types';
import 'std-env';

const I18N_MODULES = ["@nuxtjs/i18n", "nuxt-i18n-micro"];
function isUnlocalizedLocalePage(page) {
  return page._tag === "unlocalized" && typeof page.path === "string";
}
function generatePathForI18nPages(ctx) {
  const { localeCode, pageLocales, nuxtI18nConfig, forcedStrategy, normalisedLocales } = ctx;
  const locale = normalisedLocales.find((l) => l.code === localeCode);
  const strategy = forcedStrategy ?? nuxtI18nConfig.strategy;
  const i18n = toRuntimeI18nConfig({
    defaultLocale: nuxtI18nConfig.defaultLocale,
    locales: normalisedLocales,
    strategy: strategy === "prefix_and_default" ? "prefix_except_default" : strategy
  });
  const generated = localePath(pageLocales, localeCode, i18n);
  const prefixed = generated === localePath(pageLocales, localeCode, { ...i18n, strategy: "prefix" });
  const path = prefixed ? generated.slice(1) : pageLocales;
  return locale?.domain ? withHttps(withBase(path, locale.domain)) : path;
}
function splitPathForI18nLocales(path, autoI18n) {
  const selectedLocales = autoI18n.strategy === "prefix_except_default" ? autoI18n.locales.filter((l) => l.code !== autoI18n.defaultLocale) : autoI18n.locales;
  if (!path || path.startsWith("/_"))
    return path;
  const localeCodes = new Set(selectedLocales.map((locale) => locale.code));
  const runtimeI18n = toRuntimeI18nConfig(autoI18n);
  const i18n = {
    ...runtimeI18n,
    strategy: "prefix",
    locales: runtimeI18n.locales.filter((locale) => localeCodes.has(locale.code))
  };
  const normalizedPath = path.startsWith("/") ? path : `/${path}`;
  const resolved = resolveLocaleFromRoute(normalizedPath, i18n);
  const hasLocalePrefix = i18n.locales.some(
    (l) => l.code === resolved.locale && localePath(resolved.basePath, l.code, i18n) === normalizedPath
  );
  if (hasLocalePrefix)
    return path;
  return [
    path,
    ...i18n.locales.map((l) => localePath(path, l.code, i18n))
  ];
}
const COMPACT_LOCALE_PATTERN = /^\/:locale\(([^)]+)\)/;
function isCompactLocaleRoute(path) {
  return COMPACT_LOCALE_PATTERN.test(path);
}
function expandCompactLocaleRoute(path, knownLocales) {
  const match = COMPACT_LOCALE_PATTERN.exec(path);
  if (!match?.[1])
    return null;
  const locales = match[1].split("|");
  if (knownLocales?.length && !locales.some((l) => knownLocales.includes(l)))
    return null;
  return locales.map((locale) => ({
    locale,
    path: path.replace(COMPACT_LOCALE_PATTERN, `/${locale}`)
  }));
}
function normalizeLocales(nuxtI18nConfig) {
  const rawLocales = nuxtI18nConfig.locales || [];
  let onlyLocales = nuxtI18nConfig?.bundle?.onlyLocales || [];
  onlyLocales = typeof onlyLocales === "string" ? [onlyLocales] : onlyLocales;
  let locales = mergeOnKey(rawLocales.map((locale) => typeof locale === "string" ? { code: locale } : locale), "code");
  if (onlyLocales.length) {
    locales = locales.filter((locale) => onlyLocales.includes(locale.code));
  }
  return locales.map((locale) => {
    if (typeof locale.iso === "string" && !locale.language) {
      locale.language = locale.iso;
    }
    const _hreflang = locale.language || locale.code;
    const _sitemap = locale.language || locale.code;
    return { ...locale, _hreflang, _sitemap };
  });
}
function joinRoutePath(parentPath, path) {
  if (path.startsWith("/"))
    return path;
  if (!path)
    return parentPath || "/";
  return `${parentPath === "/" ? "" : parentPath.replace(/\/$/, "")}/${path}`;
}
function resolveLocalizedRouteName(name, autoI18n) {
  if (!name)
    return { name, isDefaultTree: false };
  const separator = autoI18n.routesNameSeparator || "___";
  const defaultSuffix = autoI18n.defaultLocaleRouteNameSuffix || "default";
  const segments = name.split(separator);
  const isDefaultTree = segments.at(-1) === defaultSuffix && autoI18n.locales.some((locale2) => locale2.code === segments.at(-2));
  if (isDefaultTree)
    segments.pop();
  const locale = autoI18n.locales.find((locale2) => locale2.code === segments.at(-1))?.code;
  if (locale)
    segments.pop();
  return {
    name: segments.join(separator),
    ...locale ? { locale } : {},
    isDefaultTree
  };
}
function flattenResolvedI18nRoutes(routes, autoI18n, parentPath = "") {
  return routes.flatMap((route) => {
    const path = joinRoutePath(parentPath, route.path);
    return [
      { ...resolveLocalizedRouteName(route.name, autoI18n), path, hasChildren: !!route.children?.length },
      ...flattenResolvedI18nRoutes(route.children || [], autoI18n, path)
    ];
  });
}
function normalizeI18nPageKey(key) {
  return key.replace(/^\//, "").replace(/\/index$/, "").replace(/\[{1,2}(?:\.\.\.)?([^\]]+)\]{1,2}/g, "$1").split("/").filter((segment) => !/^\([^)]+\)$/.test(segment)).join("-");
}
function routeBasePath(route, autoI18n) {
  if (!route.locale || autoI18n.strategy === "no_prefix")
    return route.path;
  return resolveLocaleFromRoute(route.path, toRuntimeI18nConfig(autoI18n), { locale: route.locale }).basePath;
}
function materializeI18nPages(autoI18n, routes) {
  const pages = autoI18n.pages;
  if (!pages)
    return void 0;
  const resolvedRoutes = flattenResolvedI18nRoutes(routes, autoI18n);
  return Object.fromEntries(Object.entries(pages).map(([pageName, pageLocales]) => {
    const normalizedPageName = normalizeI18nPageKey(pageName);
    const namedRoutes = resolvedRoutes.filter((route) => route.name === pageName || route.name === normalizedPageName);
    if (pageLocales === false) {
      const route = namedRoutes.find((route2) => route2.locale === autoI18n.defaultLocale) || namedRoutes.find((route2) => !route2.locale) || namedRoutes[0];
      return [pageName, route ? {
        _tag: "unlocalized",
        path: routeBasePath(route, autoI18n),
        ...route.hasChildren ? { subtree: true } : {}
      } : false];
    }
    if (isUnlocalizedLocalePage(pageLocales))
      return [pageName, pageLocales];
    const explicitlyMatchedRoute = resolvedRoutes.find((route) => Object.values(pageLocales).some(
      (configuredPath) => typeof configuredPath === "string" && routeBasePath(route, autoI18n) === configuredPath
    ));
    const routeGroup = namedRoutes.length ? namedRoutes : explicitlyMatchedRoute?.name ? resolvedRoutes.filter((route) => route.name === explicitlyMatchedRoute.name) : [];
    const defaultRoute = routeGroup.find((route) => route.locale === autoI18n.defaultLocale && route.isDefaultTree) || routeGroup.find((route) => route.locale === autoI18n.defaultLocale) || routeGroup.find((route) => !route.locale) || routeGroup.find((route) => route.locale && pageLocales[route.locale] === void 0);
    const originalPath = defaultRoute ? routeBasePath(defaultRoute, autoI18n) : void 0;
    const defaultPath = pageLocales[autoI18n.defaultLocale];
    const fallbackPath = typeof defaultPath === "string" ? defaultPath : originalPath;
    return [pageName, Object.fromEntries(autoI18n.locales.flatMap((locale) => {
      const configuredPath = pageLocales[locale.code];
      if (configuredPath !== void 0)
        return [[locale.code, configuredPath]];
      return fallbackPath === void 0 ? [] : [[locale.code, fallbackPath]];
    }))];
  }));
}
function mapPathForI18nPages(path, autoI18n, routes = []) {
  const pages = autoI18n.pages;
  if (!pages || !Object.keys(pages).length)
    return false;
  const materializedPages = routes.length ? materializeI18nPages(autoI18n, routes) : pages;
  const resolvedRoutes = flattenResolvedI18nRoutes(routes, autoI18n);
  const pagesForMapping = Object.fromEntries(Object.entries(materializedPages || {}).map(([pageName, pageLocales]) => {
    if (pageLocales !== false)
      return [pageName, pageLocales];
    const normalizedPageName = normalizeI18nPageKey(pageName);
    const route = resolvedRoutes.find((route2) => route2.name === pageName || route2.name === normalizedPageName);
    if (!route)
      return [pageName, false];
    const originalPath = routeBasePath(route, autoI18n);
    return [pageName, Object.fromEntries(autoI18n.locales.map((locale) => [
      locale.code,
      locale.code === autoI18n.defaultLocale ? originalPath : false
    ]))];
  }));
  const i18n = toRuntimeI18nConfig({
    ...autoI18n,
    strategy: autoI18n.strategy === "prefix_and_default" ? "prefix_except_default" : autoI18n.strategy,
    pages: pagesForMapping
  });
  const resolved = resolveLocaleAlternates(path, i18n, autoI18n.strategy === "no_prefix" ? { locale: autoI18n.defaultLocale } : {});
  if (resolved._tag === "strategy")
    return false;
  return resolved.alternates.map((alternate) => alternate.domain ? withHttps(withBase(alternate.path, alternate.domain)) : alternate.path);
}
function resolveI18nModule() {
  const found = I18N_MODULES.find((m) => hasNuxtModule(m));
  if (!found)
    return false;
  return {
    module: found,
    isMicro: found === "nuxt-i18n-micro"
  };
}
function resolveI18nPages(config, isMicro) {
  const routes = isMicro ? config.globalLocaleRoutes : config.pages;
  if (!routes)
    return void 0;
  return Object.fromEntries(
    Object.entries(routes).filter((entry) => entry[1] === false || typeof entry[1] === "object" && entry[1] !== null && !Array.isArray(entry[1]))
  );
}
async function resolveI18nConfig(logger) {
  const i18n = resolveI18nModule();
  if (!i18n)
    return false;
  if (!i18n.isMicro) {
    const i18nVersion = await getNuxtModuleVersion(i18n.module);
    if (!await hasNuxtModuleCompatibility(i18n.module, ">=8")) {
      logger?.warn(`You are using ${i18n.module} v${i18nVersion}. For the best compatibility, please upgrade to ${i18n.module} v8.0.0 or higher.`);
    }
  }
  const nuxtI18nConfig = await getNuxtModuleOptions(i18n.module) || {};
  const normalisedLocales = normalizeLocales(nuxtI18nConfig);
  const pages = resolveI18nPages(nuxtI18nConfig, i18n.isMicro);
  const usingI18nPages = Object.keys(pages || {}).length;
  const hasI18nConfigForAlternatives = nuxtI18nConfig.differentDomains || nuxtI18nConfig.multiDomainLocales || usingI18nPages || nuxtI18nConfig.strategy !== "no_prefix" && nuxtI18nConfig.locales;
  if (!hasI18nConfigForAlternatives)
    return false;
  return {
    differentDomains: nuxtI18nConfig.differentDomains,
    multiDomainLocales: nuxtI18nConfig.multiDomainLocales,
    routesNameSeparator: nuxtI18nConfig.routesNameSeparator,
    defaultLocaleRouteNameSuffix: nuxtI18nConfig.defaultLocaleRouteNameSuffix,
    defaultLocale: nuxtI18nConfig.defaultLocale,
    locales: normalisedLocales,
    strategy: nuxtI18nConfig.strategy,
    pages
  };
}
function toRuntimeI18nConfig(auto) {
  const pages = auto.pages && Object.fromEntries(
    Object.entries(auto.pages).filter((entry) => entry[1] !== false)
  );
  return {
    defaultLocale: auto.defaultLocale,
    strategy: auto.strategy,
    ...auto.differentDomains ? { differentDomains: true } : {},
    ...auto.multiDomainLocales ? { multiDomainLocales: true } : {},
    // Translated route paths. Without these the runtime can only guess
    // alternates by adding/removing a locale prefix, which is wrong for every
    // page whose slug differs per locale.
    ...pages && Object.keys(pages).length ? { pages } : {},
    locales: auto.locales.map((l) => {
      const raw = l;
      return {
        code: l.code,
        hreflang: l._hreflang || raw.language || l.code,
        name: raw.name,
        nativeName: raw.nativeName ?? raw.name,
        ...raw.language ? { language: raw.language } : {},
        ...raw.domain ? { domain: raw.domain } : {},
        ...raw.domains?.length ? { domains: [...raw.domains] } : {},
        ...raw.defaultForDomains?.length ? { defaultForDomains: [...raw.defaultForDomains] } : {}
      };
    })
  };
}
function mergeOnKey(arr, key) {
  const map = /* @__PURE__ */ new Map();
  for (const item of arr) {
    const k = item[key];
    if (map.has(k)) {
      map.set(k, { ...map.get(k), ...item });
    } else {
      map.set(k, item);
    }
  }
  return [...map.values()];
}

export { expandCompactLocaleRoute, generatePathForI18nPages, isCompactLocaleRoute, mapPathForI18nPages, materializeI18nPages, mergeOnKey, normalizeI18nPageKey, normalizeLocales, resolveI18nConfig, resolveI18nModule, splitPathForI18nLocales, toRuntimeI18nConfig };
