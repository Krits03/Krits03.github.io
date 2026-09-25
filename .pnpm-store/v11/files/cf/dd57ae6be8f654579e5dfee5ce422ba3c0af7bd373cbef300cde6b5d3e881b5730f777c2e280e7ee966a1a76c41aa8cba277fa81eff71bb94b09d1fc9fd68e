import { SitemapUrlInput, SitemapUrl } from '../dist/runtime/types.js';
export * from '../dist/runtime/types.js';
import { SitemapInput } from 'sitemapd/parse';
export { CollectSitemapResult, ParseSitemapOptions, SitemapCompleteness, SitemapDocument, SitemapDocumentKind, SitemapExtensions, SitemapFormat, SitemapInput, SitemapIssue, SitemapIssueCode, SitemapParseEvent, SitemapReference, SitemapUrlRecord, collectSitemap, parseSitemap } from 'sitemapd/parse';
export { SitemapDocumentLoadResult, SitemapDocumentLoader, SitemapLoadFailureCode, SitemapLoadRequest, SitemapLoadSource, SitemapReadOptions, SitemapReadResult, SitemapReader, SitemapReaderOptions, SitemapTargetAuthorization, SitemapTargetAuthorizer, SitemapWalkDocument, SitemapWalkDocumentVisitor, SitemapWalkFailure, SitemapWalkNonRetainedResult, SitemapWalkOptions, SitemapWalkPartialReason, SitemapWalkResult, SitemapWalkRetainedResult, createSitemapReader } from 'sitemapd';
export { FetchDocumentLoaderOptions, SitemapFetch, createFetchDocumentLoader } from 'sitemapd/fetch';

/** @deprecated Use `SitemapIssue` with `parseSitemap` or `collectSitemap`. */
interface SitemapWarning {
    type: 'validation';
    message: string;
    context?: {
        url?: string;
        field?: string;
        value?: unknown;
    };
}
/** @deprecated Use the tagged `CollectSitemapResult` returned by `collectSitemap`. */
interface SitemapParseResult {
    urls: SitemapUrlInput[];
    warnings: SitemapWarning[];
}
/** @deprecated Use `SitemapReference`. */
interface SitemapIndexEntry {
    loc: string;
    lastmod?: string;
}
/** @deprecated Use the tagged `CollectSitemapResult` returned by `collectSitemap`. */
interface SitemapIndexParseResult {
    entries: SitemapIndexEntry[];
    warnings: SitemapWarning[];
}
/** @deprecated Use `SitemapInput`. */
type SitemapXmlChunk = string | Uint8Array;
/** @deprecated Use `SitemapInput`. */
type SitemapXmlInput = SitemapInput;
/** @deprecated Use `ParseSitemapOptions`. */
interface SitemapStreamOptions {
    maxEntryBytes?: number;
    maxBufferBytes?: number;
}
/** @deprecated Use `SitemapParseEvent`. */
type SitemapXmlStreamEvent = {
    _tag: 'url';
    url: SitemapUrlInput;
} | {
    _tag: 'warning';
    warning: SitemapWarning;
};
/** @deprecated Use `SitemapParseEvent`. */
type SitemapIndexStreamEvent = {
    _tag: 'sitemap';
    sitemap: SitemapIndexEntry;
} | {
    _tag: 'warning';
    warning: SitemapWarning;
};
/** @deprecated Use `SitemapDocumentKind`. */
type SitemapKind = 'urlset' | 'index';
/** @deprecated Use `SitemapParseEvent`. */
type SitemapStreamEvent = {
    _tag: 'kind';
    kind: SitemapKind;
} | SitemapXmlStreamEvent | SitemapIndexStreamEvent;
/**
 * @deprecated Use `parseSitemap` from `@nuxtjs/sitemap/utils`. Canonical
 * streams emit `document`, `url`, `sitemap`, `issue`, and terminal `end`
 * events. URL and sitemap payloads use `entry`.
 */
declare function parseSitemapStream(input: SitemapXmlInput, options?: SitemapStreamOptions): AsyncGenerator<SitemapStreamEvent>;
/**
 * @deprecated Use `parseSitemap` from `@nuxtjs/sitemap/utils` and handle
 * events whose document kind is `urlset`.
 */
declare function parseSitemapXmlStream(input: SitemapXmlInput, options?: SitemapStreamOptions): AsyncGenerator<SitemapXmlStreamEvent>;
/**
 * @deprecated Use `parseSitemap` from `@nuxtjs/sitemap/utils` and handle
 * events whose document kind is `index`.
 */
declare function parseSitemapIndexStream(input: SitemapXmlInput, options?: SitemapStreamOptions): AsyncGenerator<SitemapIndexStreamEvent>;
/**
 * @deprecated Use `collectSitemap` from `@nuxtjs/sitemap/utils` and handle
 * its tagged result.
 */
declare function parseSitemapXml(xml: string): Promise<SitemapParseResult>;
/**
 * @deprecated Use `collectSitemap` from `@nuxtjs/sitemap/utils` and handle
 * an `index` document result.
 */
declare function parseSitemapIndex(xml: string): Promise<SitemapIndexParseResult>;
/**
 * @deprecated Use `collectSitemap` from `@nuxtjs/sitemap/utils` and inspect
 * the tagged document result.
 */
declare function isSitemapIndex(xml: string): boolean;

declare function parseHtmlExtractSitemapMeta(html: string, options?: {
    images?: boolean;
    videos?: boolean;
    lastmod?: boolean;
    alternatives?: boolean;
    resolveUrl?: (s: string) => string;
}): Partial<SitemapUrl> | null;

export { isSitemapIndex, parseHtmlExtractSitemapMeta, parseSitemapIndex, parseSitemapIndexStream, parseSitemapStream, parseSitemapXml, parseSitemapXmlStream };
export type { SitemapIndexEntry, SitemapIndexParseResult, SitemapIndexStreamEvent, SitemapKind, SitemapParseResult, SitemapStreamEvent, SitemapStreamOptions, SitemapWarning, SitemapXmlChunk, SitemapXmlInput, SitemapXmlStreamEvent };
