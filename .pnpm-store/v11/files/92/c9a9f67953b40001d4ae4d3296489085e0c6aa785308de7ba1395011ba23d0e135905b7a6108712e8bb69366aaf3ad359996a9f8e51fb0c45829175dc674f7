import { ComputedRef, Ref } from 'vue';

declare const SiteConfigPriority: {
    readonly system: -15;
    readonly vendor: -5;
    readonly nitro: -4;
    readonly config: -3;
    readonly i18n: -2;
    readonly build: -1;
    readonly runtime: 0;
};

interface SiteConfigResolved {
    /**
     * The canonical Site URL.
     *
     * - Build / Prerender: Inferred from CI environment (Netlify, Vercel)
     * - SSR: Inferred from request headers
     * - SPA: Inferred from `window.location`
     *
     * Used by: nuxt-simple-sitemap, nuxt-simple-robots, nuxt-schema-org, nuxt-og-image, etc.
     */
    url?: string;
    /**
     * The name of the site.
     *
     * - Build / Prerender: Inferred from CI environment (Netlify)
     *
     * Used by: nuxt-schema-org, nuxt-seo-kit
     */
    name?: string;
    /**
     * Whether the site is indexable by search engines.
     *
     * Allows you to opt-out productions environment from being indexed.
     */
    indexable?: boolean;
    /**
     * The environment of the site. Comparable to `process.env.NODE_ENV`.
     */
    env?: 'production' | 'staging' | 'development' | 'preview' | 'uat' | string;
    /**
     * Whether the site uses trailing slash.
     */
    trailingSlash?: boolean;
    /**
     * The mapping of the context of each site config value being set.
     */
    _context?: Record<string, string>;
    /**
     * Support any keys as site config.
     */
    [key: string]: any;
}
/**
 * @deprecated use SiteConfigResolved
 */
type SiteConfig = SiteConfigResolved;
type MaybeComputedRef<T> = T | (() => T) | ComputedRef<T> | Ref<T>;
type MaybeComputedRefEntries<T> = {
    [key in keyof T]?: MaybeComputedRef<T[key]>;
};
/**
 * Strip the string index signature from a type so mapped types preserve
 * the declared named keys (required for autocomplete and type checking).
 */
type KnownKeys<T> = {
    [K in keyof T as string extends K ? never : number extends K ? never : K]: T[K];
};
type SiteConfigInput = Omit<MaybeComputedRefEntries<KnownKeys<SiteConfigResolved>>, '_context' | 'indexable'> & {
    _context?: string;
    _priority?: number;
    indexable?: MaybeComputedRef<string | boolean>;
    [key: string]: any;
};
interface GetSiteConfigOptions {
    debug?: boolean;
    skipNormalize?: boolean;
    resolveRefs?: boolean;
}
interface SiteConfigStack {
    stack: Partial<SiteConfigInput>[];
    push: (config: SiteConfigInput) => () => void;
    get: (options?: GetSiteConfigOptions) => SiteConfigResolved;
}

declare function normalizeSiteConfig(config: SiteConfigResolved): SiteConfigResolved;
declare function validateSiteConfigStack(stack: SiteConfigStack, options?: {
    dev?: boolean;
}): string[];
declare function createSiteConfigStack(options?: {
    debug: boolean;
}): {
    stack: Partial<SiteConfigInput>[];
    push: (input: SiteConfigInput | SiteConfigResolved) => () => void;
    get: (options?: GetSiteConfigOptions) => SiteConfigResolved;
};

/**
 * `toValue` without importing `vue`.
 *
 * Site config values are refs, computeds, getters or plain values, so resolving
 * one needs `toValue` — but importing it from `vue` costs the whole framework.
 * `vue` re-exports it from `@vue/runtime-dom`, so a single named import pulls
 * `@vue/runtime-dom` + `@vue/runtime-core` (~246 KB) into whatever graph asks
 * for it. On the server that graph is a Nitro plugin, which on a Cloudflare
 * Worker is evaluated at cold start, before the isolate can answer any request:
 * the renderer, the scheduler and the component system all initialise so that
 * one pure function can unwrap a value.
 *
 * `@vue/reactivity` is where `toValue` actually lives and is a tenth the size,
 * but `vue` reaches it through `@vue/runtime-dom` rather than depending on it
 * directly, so importing it here would make every consumer install a peer.
 * Nine lines is a better trade than that.
 *
 * `__v_isRef` is the same marker Vue's own `isRef` reads, and it is how every
 * other library in the ecosystem (VueUse's `unref`, for one) recognises a ref
 * without a hard dependency on Vue.
 */
declare function toValue<T>(source: T | (() => T) | {
    __v_isRef?: true;
    value: T;
}): T;
declare function envSiteConfig(env?: Record<string, any>): Record<string, any>;

export { SiteConfigPriority, createSiteConfigStack, envSiteConfig, normalizeSiteConfig, toValue, validateSiteConfigStack };
export type { GetSiteConfigOptions, MaybeComputedRef, MaybeComputedRefEntries, SiteConfig, SiteConfigInput, SiteConfigResolved, SiteConfigStack };
