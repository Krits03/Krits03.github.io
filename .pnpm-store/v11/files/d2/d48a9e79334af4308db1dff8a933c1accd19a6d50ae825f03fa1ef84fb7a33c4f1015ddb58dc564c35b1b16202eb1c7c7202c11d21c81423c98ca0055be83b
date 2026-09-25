import type { ModuleRuntimeConfig, NitroUrlResolvers, SitemapIndexEntry } from '../../../types.js';
export declare function renderSitemapIndexXmlChunks(sitemaps: SitemapIndexEntry[], resolvers: NitroUrlResolvers, { version, xsl, credits, minify }: Pick<ModuleRuntimeConfig, 'version' | 'xsl' | 'credits' | 'minify'>, errorInfo?: {
    messages: string[];
    urls: string[];
}): Generator<string>;
export declare function urlsToIndexXml(sitemaps: SitemapIndexEntry[], resolvers: NitroUrlResolvers, { version, xsl, credits, minify }: Pick<ModuleRuntimeConfig, 'version' | 'xsl' | 'credits' | 'minify'>, errorInfo?: {
    messages: string[];
    urls: string[];
}): string;
export declare function urlsToIndexXmlStream(sitemaps: SitemapIndexEntry[], resolvers: NitroUrlResolvers, config: Pick<ModuleRuntimeConfig, 'version' | 'xsl' | 'credits' | 'minify'>, errorInfo?: {
    messages: string[];
    urls: string[];
}): ReadableStream<Uint8Array>;
