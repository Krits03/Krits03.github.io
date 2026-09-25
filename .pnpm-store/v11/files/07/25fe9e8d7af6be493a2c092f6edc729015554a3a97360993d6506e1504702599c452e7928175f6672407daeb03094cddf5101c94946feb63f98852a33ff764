/**
 * Runtime-safe i18n route resolution.
 *
 * `./i18n` reaches for `@nuxt/kit` to read the installed module's options, so it
 * can only run at build time. This entry carries no build-time dependencies and
 * is importable from a module's runtime (nitro handlers, plugins, composables).
 * Feed it the config `toRuntimeI18nConfig()` produces.
 */
/**
 * Resolved route paths keyed by route name, then locale code. Per-locale
 * `false` disables that locale. A tagged unlocalized entry represents i18n's
 * whole-route `false` after build-time materialization.
 *
 * ```
 * { about: { en: '/about', fr: '/a-propos' }, admin: { _tag: 'unlocalized', path: '/admin' } }
 * ```
 */
type LocalePagePaths = Record<string, string | false>;
interface UnlocalizedLocalePage {
    /** Route excluded from i18n localization by a whole-route `pages` false. */
    _tag: 'unlocalized';
    /** Original resolved Nuxt route pattern. */
    path: string;
    /** The route has children, which i18n also leaves unlocalized. */
    subtree?: true;
}
type LocalePages = Record<string, LocalePagePaths | UnlocalizedLocalePage | undefined>;
interface RuntimeLocale {
    code: string;
    hreflang: string;
    name?: string;
    nativeName?: string;
    language?: string;
    domain?: string;
    domains?: string[];
    defaultForDomains?: string[];
}
/** Runtime-safe subset of `AutoI18nConfig` used for route locale resolution. */
interface RuntimeI18nConfig {
    defaultLocale: string;
    strategy: 'no_prefix' | 'prefix_except_default' | 'prefix' | 'prefix_and_default';
    locales: RuntimeLocale[];
    differentDomains?: boolean;
    multiDomainLocales?: boolean;
    /** Translated route paths, when i18n is configured with custom routes. */
    pages?: LocalePages;
}
interface LocaleAlternate {
    code: string;
    hreflang: string;
    path: string;
    domain?: string;
}
type LocaleAlternateResolution = {
    _tag: 'pages';
    alternates: LocaleAlternate[];
} | {
    _tag: 'strategy';
    alternates: LocaleAlternate[];
};
interface RouteLocaleInfo {
    /** Resolved locale code for this route */
    locale: string;
    /** Route with locale prefix stripped (e.g. /fr/about → /about). For no_prefix this equals route. */
    basePath: string;
}
interface RuntimeRouteContext {
    /** Request host, used to resolve locales under domain-based strategies. */
    host?: string;
    /** Known current locale, required to translate no_prefix routes without a locale domain. */
    locale?: string;
}
/**
 * Resolve the canonical domain for a locale. Domainless locales are served on
 * every domain, so their stable canonical is the default locale's domain.
 */
declare function resolveCanonicalLocaleDomain(locale: RuntimeLocale | undefined, defaultLocale?: RuntimeLocale): string | undefined;
/**
 * Resolve which locale a route belongs to and the locale-stripped base path.
 */
declare function resolveLocaleFromRoute(route: string, i18n: RuntimeI18nConfig, context?: RuntimeRouteContext): RouteLocaleInfo;
/**
 * Build the URL path for a base path under a given locale, honoring the i18n strategy.
 */
declare function localePath(basePath: string, locale: string, i18n: RuntimeI18nConfig, context?: RuntimeRouteContext): string;
/**
 * Compute hreflang alternates for a given route.
 * Returns the route itself plus all sibling locale variants.
 *
 * Translated slugs (i18n `pages`) can't be derived by adding or removing a
 * locale prefix — `/about` and `/fr/a-propos` are the same page — so the route
 * table is consulted first and prefix arithmetic is the fallback.
 */
declare function resolveLocaleAlternates(route: string, i18n: RuntimeI18nConfig, context?: RuntimeRouteContext): LocaleAlternateResolution;
declare function computeLocaleAlternates(route: string, i18n: RuntimeI18nConfig, context?: RuntimeRouteContext): LocaleAlternate[];

export { computeLocaleAlternates, localePath, resolveCanonicalLocaleDomain, resolveLocaleAlternates, resolveLocaleFromRoute };
export type { LocaleAlternate, LocaleAlternateResolution, LocalePagePaths, LocalePages, RouteLocaleInfo, RuntimeI18nConfig, RuntimeLocale, RuntimeRouteContext, UnlocalizedLocalePage };
