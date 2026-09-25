import type { ActiveHeadEntry, Head, VueHeadClient } from '@unhead/vue';
import type { NuxtSSRContext } from 'nuxt/app';
import type { OgImageOptions, OgImageOptionsInternal, OgImagePrebuilt, OgImageRuntimeConfig } from '../types.js';
/**
 * Payload format: [ogKey, options, basePath]
 * basePath is stored so the lazy meta() callback can rebuild URLs
 * after injecting head-derived title/description.
 */
type OgImagePayload = [string, OgImageOptionsInternal, string];
declare module 'nuxt/app' {
    interface NuxtSSRContext {
        _ogImagePayloads?: OgImagePayload[];
        _ogImageInstance?: ActiveHeadEntry<Head>;
        _ogImageDevtoolsInstance?: ActiveHeadEntry<Head>;
    }
}
export declare function setHeadOgImagePrebuilt(input: OgImagePrebuilt): void;
export declare function createOgImageMeta(src: string, input: OgImageOptions | OgImagePrebuilt, ssrContext: NuxtSSRContext, pagePath?: string, head?: VueHeadClient): void;
export declare function resolveComponentName(component: OgImageOptionsInternal['component']): OgImageOptionsInternal['component'];
export interface GetOgImagePathResult {
    path: string;
    hash?: string;
}
/**
 * @deprecated Use the return value of `defineOgImage()` instead, which now returns an array of generated paths.
 */
export declare function getOgImagePath(_pagePath: string, _options?: Partial<OgImageOptionsInternal>): GetOgImagePathResult;
export declare function useOgImageRuntimeConfig(): OgImageRuntimeConfig;
export {};
