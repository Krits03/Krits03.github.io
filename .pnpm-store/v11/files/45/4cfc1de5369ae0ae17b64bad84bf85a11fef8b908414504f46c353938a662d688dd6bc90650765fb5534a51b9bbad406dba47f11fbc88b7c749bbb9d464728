import type { ModuleRuntimeConfig, NitroUrlResolvers, ResolvedSitemapUrl } from '../../../types.js';
export declare function escapeValueForXml(value: boolean | string | number): string;
export declare function renderSitemapXmlChunks(urls: ResolvedSitemapUrl[], resolvers: NitroUrlResolvers, config: Pick<ModuleRuntimeConfig, 'version' | 'xsl' | 'credits' | 'minify'>, errorInfo?: {
    messages: string[];
    urls: string[];
}): Generator<string>;
export declare function urlsToXml(urls: ResolvedSitemapUrl[], resolvers: NitroUrlResolvers, config: Pick<ModuleRuntimeConfig, 'version' | 'xsl' | 'credits' | 'minify'>, errorInfo?: {
    messages: string[];
    urls: string[];
}): string;
export declare function urlsToXmlStream(urls: ResolvedSitemapUrl[], resolvers: NitroUrlResolvers, config: Pick<ModuleRuntimeConfig, 'version' | 'xsl' | 'credits' | 'minify'>, errorInfo?: {
    messages: string[];
    urls: string[];
}): ReadableStream<Uint8Array>;
