import type { ModuleRuntimeConfig, NitroUrlResolvers, ResolvedSitemapUrl, SitemapDefinition } from '../../../types.js';
type NitroApp = ReturnType<typeof import('#nuxtseo/nitro').useNitroApp>;
export interface ResolvedSitemapUrlsResult {
    urls: ResolvedSitemapUrl[];
    failedSources: Array<{
        url: string;
        error: string;
    }>;
}
export declare function buildResolvedSitemapUrls(effectiveSitemap: SitemapDefinition, matchName: string, isChunked: boolean, resolvers: NitroUrlResolvers, runtimeConfig: ModuleRuntimeConfig, nitro?: NitroApp): Promise<ResolvedSitemapUrlsResult>;
export declare const buildResolvedSitemapUrlsCached: any;
export declare function getResolvedSitemapUrls(effectiveSitemap: SitemapDefinition, matchName: string, isChunked: boolean, resolvers: NitroUrlResolvers, runtimeConfig: ModuleRuntimeConfig, nitro?: NitroApp): Promise<ResolvedSitemapUrlsResult>;
export declare function buildSitemapUrls(sitemap: SitemapDefinition, resolvers: NitroUrlResolvers, runtimeConfig: ModuleRuntimeConfig, nitro?: NitroApp): Promise<ResolvedSitemapUrlsResult>;
export { urlsToXml, urlsToXmlStream } from './xml.js';
