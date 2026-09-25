import { LocaleObject, NuxtI18nOptions } from '@nuxtjs/i18n';
import { UnlocalizedLocalePage, RuntimeI18nConfig } from './i18n-runtime.mjs';
export { LocaleAlternate, LocaleAlternateResolution, LocalePagePaths, LocalePages, RouteLocaleInfo, RuntimeLocale, RuntimeRouteContext } from './i18n-runtime.mjs';

declare const I18N_MODULES: readonly ["@nuxtjs/i18n", "nuxt-i18n-micro"];
type I18nModuleName = typeof I18N_MODULES[number];
type Strategies = 'no_prefix' | 'prefix_except_default' | 'prefix' | 'prefix_and_default';
type NormalisedLocale = LocaleObject & {
    _sitemap: string;
    _hreflang: string;
};
interface AutoI18nConfig {
    locales: NormalisedLocale[];
    defaultLocale: string;
    strategy: Strategies;
    differentDomains?: boolean;
    multiDomainLocales?: boolean;
    routesNameSeparator?: string;
    defaultLocaleRouteNameSuffix?: string;
    pages?: Record<string, Record<string, string | false> | UnlocalizedLocalePage | false>;
}
type I18nPages = NonNullable<AutoI18nConfig['pages']>;
interface StrategyProps {
    localeCode: string;
    pageLocales: string;
    nuxtI18nConfig: NuxtI18nOptions;
    forcedStrategy?: Strategies;
    normalisedLocales: AutoI18nConfig['locales'];
}
declare function generatePathForI18nPages(ctx: StrategyProps): string;
declare function splitPathForI18nLocales(path: string, autoI18n: AutoI18nConfig): string | string[];
interface ExpandedLocaleRoute {
    locale: string;
    path: string;
}
/**
 * Detect a compacted i18n route such as `/:locale(en|fr)/about`.
 *
 * Both `nuxt-i18n-micro` and `@nuxtjs/i18n` (experimental `compactRoutes`) collapse
 * per-locale routes into a single regex route using this syntax, so route-table
 * consumers (sitemap, link-checker) see one `:locale(...)` route instead of one per
 * locale.
 */
declare function isCompactLocaleRoute(path: string): boolean;
/**
 * Expand a compacted i18n route into one entry per locale.
 *
 * `/:locale(en|fr)/about` -> `[{ locale: 'en', path: '/en/about' }, { locale: 'fr', path: '/fr/about' }]`
 *
 * Pass `knownLocales` to guard against a genuine `:locale` route param: when provided,
 * expansion only runs if at least one captured token is a real locale code. Returns
 * `null` when the path is not a compacted locale route.
 */
declare function expandCompactLocaleRoute(path: string, knownLocales?: string[]): ExpandedLocaleRoute[] | null;
declare function normalizeLocales(nuxtI18nConfig: NuxtI18nOptions): AutoI18nConfig['locales'];
interface ResolvedI18nRoute {
    name?: string;
    path: string;
    children?: ResolvedI18nRoute[];
}
/** Normalize an i18n `pages` key to the corresponding resolved Nuxt route name. Build-time only. */
declare function normalizeI18nPageKey(key: string): string;
/**
 * Complete partial i18n `pages` entries from Nuxt's resolved route table.
 *
 * Route names are identifiers, not URL paths. The resolved route path is the
 * only safe fallback for nested, dynamic, grouped, or custom Nuxt routes.
 * Whole-route `false` becomes a tagged entry carrying that resolved path.
 */
declare function materializeI18nPages(autoI18n: AutoI18nConfig, routes: readonly ResolvedI18nRoute[]): I18nPages | undefined;
declare function mapPathForI18nPages(path: string, autoI18n: AutoI18nConfig, routes?: readonly ResolvedI18nRoute[]): string[] | false;
interface I18nModuleResolution {
    module: I18nModuleName;
    isMicro: boolean;
}
/**
 * Detect which i18n module is installed (@nuxtjs/i18n or nuxt-i18n-micro).
 *
 * Returns `false` when neither is installed.
 */
declare function resolveI18nModule(): false | I18nModuleResolution;
declare function resolveI18nConfig(logger?: {
    warn: (msg: string) => void;
}): Promise<false | AutoI18nConfig>;
/**
 * Strip a build-time i18n config down to what `./i18n-runtime` needs, dropping
 * the non-serializable `LocaleObject` extras so it can be handed to the runtime
 * through `runtimeConfig`. Materialize partial and whole-route-false `pages`
 * entries before calling this function; unresolved whole-route false entries
 * are omitted instead of becoming fabricated runtime URLs.
 */
declare function toRuntimeI18nConfig(auto: AutoI18nConfig): RuntimeI18nConfig;
declare function mergeOnKey<T extends Record<string, any>>(arr: T[], key: keyof T): T[];

export { RuntimeI18nConfig, UnlocalizedLocalePage, expandCompactLocaleRoute, generatePathForI18nPages, isCompactLocaleRoute, mapPathForI18nPages, materializeI18nPages, mergeOnKey, normalizeI18nPageKey, normalizeLocales, resolveI18nConfig, resolveI18nModule, splitPathForI18nLocales, toRuntimeI18nConfig };
export type { AutoI18nConfig, ExpandedLocaleRoute, I18nModuleResolution, NormalisedLocale, ResolvedI18nRoute, Strategies, StrategyProps };
