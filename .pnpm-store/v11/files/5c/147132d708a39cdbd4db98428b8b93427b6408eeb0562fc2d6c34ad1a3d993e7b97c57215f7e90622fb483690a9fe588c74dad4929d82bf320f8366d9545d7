import type { AlternativeEntry, AutoI18nConfig, FilterInput } from './types.js';
export { createFilter, type CreateFilterOptions } from 'nuxtseo-shared/utils';
export declare const logger: import("consola").ConsolaInstance;
export declare function xmlEscape(value: string | number | boolean | Date): string;
export declare function mergeOnKey<T, K extends keyof T>(arr: T[], key: K, onMerge?: (key: T[K]) => void): T[];
export declare function splitForLocales(path: string, locales: readonly string[] | Set<string>): [string | null, string];
export interface ResolvedI18nRouteEntry {
    locale: AutoI18nConfig['locales'][number];
    loc: string;
    alternatives: AlternativeEntry[];
}
export declare function resolveI18nRouteEntries(route: string, i18n: AutoI18nConfig, includeHref?: (href: string) => boolean): ResolvedI18nRouteEntry[];
/**
 * Resolve which locale a multi-sitemap name belongs to.
 *
 * i18n-mapped sitemaps are named either `<localeSitemap>` (default) or
 * `<localeSitemap>-<name>` (custom sitemaps). Locale `_sitemap` keys can share a
 * prefix (e.g. `zh` and `zh-Hant`), so a naive `name.startsWith(`${key}-`)` check
 * collides: `zh-Hant` would match the `zh` locale. Resolve by the longest matching
 * key to disambiguate.
 */
export declare function resolveI18nSitemapLocaleKey(sitemapName: string, localeSitemapKeys: string[]): string | null;
/**
 * Transform a literal notation string regex to RegExp
 */
export declare function normalizeRuntimeFilters(input?: FilterInput[]): (RegExp | string)[];
export declare function createPathFilter(options?: {
    include?: (FilterInput | string | RegExp)[];
    exclude?: (FilterInput | string | RegExp)[];
}, baseURL?: string): (loc: string, pathname?: string) => boolean;
