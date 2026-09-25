import * as _nuxt_schema from '@nuxt/schema';
import { ModuleRuntimeConfig, ModuleOptions as ModuleOptions$1 } from '../dist/runtime/types.js';
export * from '../dist/runtime/types.js';

declare global {
    var __sitemapCollectionFilters: Map<string, (entry: any) => boolean> | undefined;
    var __sitemapCollectionOnUrlFns: Map<string, (url: any, entry: any, collection: string) => void> | undefined;
}

interface ModuleOptions extends ModuleOptions$1 {
}
interface ModuleHooks {
    /**
     * Hook called after the prerender of the sitemaps is done.
     */
    'sitemap:prerender:done': (ctx: {
        options: ModuleRuntimeConfig;
        sitemaps: {
            name: string;
            readonly content: string;
        }[];
    }) => void | Promise<void>;
}
declare module '@nuxt/schema' {
    interface NuxtHooks extends ModuleHooks {
    }
}
declare const _default: _nuxt_schema.NuxtModule<ModuleOptions, ModuleOptions, false>;

export { _default as default };
export type { ModuleHooks, ModuleOptions };
