import type { H3Event } from '#nuxtseo/h3';
import type { ModuleRuntimeConfig, NitroUrlResolvers, SitemapDefinition } from '../../types.js';
import { useNitroApp } from '#nuxtseo/nitro';
type NitroApp = ReturnType<typeof useNitroApp>;
export declare function useNitroUrlResolvers(e: H3Event): NitroUrlResolvers;
export declare function renderSitemapOutput(nitro: NitroApp, event: H3Event, sitemapName: string, renderString: () => string, renderStream: () => ReadableStream<Uint8Array>, shouldStream: boolean, debug: boolean): Promise<string | ReadableStream<Uint8Array>>;
export declare function setSitemapResponseHeaders(event: H3Event, runtimeConfig: ModuleRuntimeConfig): void;
export declare function createSitemap(event: H3Event, definition: SitemapDefinition, runtimeConfig: ModuleRuntimeConfig): Promise<string | ReadableStream<Uint8Array<ArrayBufferLike>>>;
export {};
