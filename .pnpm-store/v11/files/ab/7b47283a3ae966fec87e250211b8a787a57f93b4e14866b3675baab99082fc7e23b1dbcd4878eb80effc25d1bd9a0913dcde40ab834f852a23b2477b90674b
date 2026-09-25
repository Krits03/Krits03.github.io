import { S as SitemapDocumentLoader } from './shared/sitemapd.BccTYgMw.mjs';
export { a as SitemapDocumentLoadResult, b as SitemapLoadRequest } from './shared/sitemapd.BccTYgMw.mjs';
import './shared/sitemapd.pCEkgy4I.mjs';

type SitemapFetch = (input: string, init: RequestInit) => Promise<{
    ok: boolean;
    status: number;
    statusText: string;
    headers: Pick<Headers, 'get'>;
    body: ReadableStream<Uint8Array> | null;
}>;
interface FetchDocumentLoaderOptions {
    fetch: SitemapFetch;
    headers?: HeadersInit;
}
/**
 * Generic Fetch adapter. It deliberately makes no DNS or network-authority
 * security claim. The reader's required target authorizer owns that policy.
 */
declare function createFetchDocumentLoader(options: FetchDocumentLoaderOptions): SitemapDocumentLoader;

export { SitemapDocumentLoader, createFetchDocumentLoader };
export type { FetchDocumentLoaderOptions, SitemapFetch };
