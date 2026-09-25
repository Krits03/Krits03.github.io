import type { NitroUrlResolvers, ResolvedSitemapUrl, SitemapUrl, SitemapUrlInput } from '../../../types.js';
export declare function validateSitemapUrl(url: SitemapUrlInput): string[];
export declare function preNormalizeEntry(_e: SitemapUrl | string, resolvers?: NitroUrlResolvers): ResolvedSitemapUrl;
export declare function isEncoded(url: string): boolean;
interface NormaliseCache {
    lastmodInput?: string | Date;
    lastmodOutput?: string | false;
}
export declare function normaliseEntry(_e: ResolvedSitemapUrl, defaults?: Omit<SitemapUrl, 'loc'>, resolvers?: NitroUrlResolvers, cache?: NormaliseCache): ResolvedSitemapUrl;
export declare function isValidW3CDate(d: string): boolean;
export declare function normaliseDate(date: string | Date): string;
export {};
