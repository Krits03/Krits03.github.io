import { f as SitemapInput, P as ParseSitemapOptions, b as SitemapDocument, C as CollectSitemapResult, i as SitemapUrlRecord, S as SitemapReference } from './sitemapd.pCEkgy4I.js';

type SitemapLoadSource = 'root' | 'redirect' | 'index_child' | 'robots';
interface SitemapLoadRequest {
    url: string;
    resource: 'sitemap' | 'robots';
    source: SitemapLoadSource;
    depth: number;
    parentUrl?: string;
    signal?: AbortSignal;
    maxWireBytes?: number;
}
type SitemapLoadFailureCode = 'timeout' | 'cancelled' | 'wire_limit' | 'content_type' | 'network';
type SitemapDocumentLoadResult = {
    _tag: 'body';
    url: string;
    body: SitemapInput;
} | {
    _tag: 'redirect';
    url: string;
    location: string;
    status: number;
} | {
    _tag: 'not_found';
    url: string;
    status: 404 | 410;
} | {
    _tag: 'http_error';
    url: string;
    status: number;
    statusText: string;
} | {
    _tag: 'load_error';
    url: string;
    code: SitemapLoadFailureCode;
    detail: string;
    bytesRead?: number;
};
type SitemapDocumentLoader = (request: SitemapLoadRequest) => Promise<SitemapDocumentLoadResult>;
type SitemapTargetAuthorization = {
    _tag: 'allow';
} | {
    _tag: 'deny';
    reason: string;
};
type SitemapTargetAuthorizer = (request: SitemapLoadRequest) => SitemapTargetAuthorization | Promise<SitemapTargetAuthorization>;
interface SitemapReaderOptions {
    loadDocument: SitemapDocumentLoader;
    authorizeTarget: SitemapTargetAuthorizer;
    limits?: {
        maxWireBytes?: number;
        maxDecodedBytes?: number;
        maxEntries?: number;
        maxRedirects?: number;
        maxDepth?: number;
        maxDocuments?: number;
        maxUrls?: number;
    };
}
interface SitemapReadOptions extends ParseSitemapOptions {
    maxWireBytes?: number;
    maxRedirects?: number;
    signal?: AbortSignal;
    source?: SitemapLoadSource;
    depth?: number;
    parentUrl?: string;
}
type SitemapReadResult = {
    _tag: 'ok';
    url: string;
    document: SitemapDocument;
    parse: Extract<CollectSitemapResult, {
        _tag: 'document';
    }>;
} | {
    _tag: 'not_found';
    url: string;
    status: 404 | 410;
} | {
    _tag: 'failure';
    url: string;
    reason: 'unauthorized' | 'redirect_limit' | 'invalid_redirect' | 'http' | 'load' | 'document';
    detail: string;
    code?: SitemapLoadFailureCode;
    status?: number;
};
interface SitemapWalkOptions extends SitemapReadOptions {
    maxDepth?: number;
    maxDocuments?: number;
    maxUrls?: number;
    concurrency?: number;
    retention?: 'all' | 'none';
    /** Documents committed by an earlier bounded round. */
    seenDocuments?: readonly string[];
    onDocument?: SitemapWalkDocumentVisitor;
}
type SitemapWalkEntry = {
    url: string;
    depth: 0;
    source: 'root';
    parentUrl?: never;
} | {
    url: string;
    depth: number;
    source: 'index_child';
    parentUrl: string;
};
type SitemapWalkInput = string | readonly string[] | readonly SitemapWalkEntry[];
interface SitemapWalkDocument {
    requestedUrl: string;
    resolvedUrl: string;
    source: SitemapLoadSource;
    depth: number;
    parentUrl?: string;
    document: SitemapDocument;
    parse: Extract<CollectSitemapResult, {
        _tag: 'document';
    }>;
}
type SitemapWalkDocumentVisitor = (document: SitemapWalkDocument) => void | Promise<void>;
type SitemapWalkFailure = SitemapWalkEntry & {
    result: Exclude<SitemapReadResult, {
        _tag: 'ok';
    }>;
};
type SitemapWalkPartialReason = 'read_failure' | 'depth_limit' | 'document_limit' | 'url_limit' | 'document_partial' | 'cancelled';
interface SitemapWalkBaseData {
    urlsObserved: number;
    referencesObserved: number;
    documentsAttempted: number;
    documentsRead: number;
    failures: SitemapWalkFailure[];
    /** Breadth-first work not committed before this bounded round stopped. */
    frontier: SitemapWalkEntry[];
}
type SitemapWalkStatus = {
    _tag: 'complete';
} | {
    _tag: 'partial';
    reasons: SitemapWalkPartialReason[];
};
type SitemapWalkRetainedResult = SitemapWalkStatus & SitemapWalkBaseData & {
    entriesRetained: true;
    entries: SitemapUrlRecord[];
    references: SitemapReference[];
};
type SitemapWalkNonRetainedResult = SitemapWalkStatus & SitemapWalkBaseData & {
    entriesRetained: false;
    entries: [];
    references: [];
};
type SitemapWalkResult = SitemapWalkRetainedResult | SitemapWalkNonRetainedResult;
interface SitemapReader {
    read: (url: string, options?: SitemapReadOptions) => Promise<SitemapReadResult>;
    walk: {
        (input: SitemapWalkInput, options: SitemapWalkOptions & {
            retention: 'none';
        }): Promise<SitemapWalkNonRetainedResult>;
        (input: SitemapWalkInput, options?: SitemapWalkOptions & {
            retention?: 'all';
        }): Promise<SitemapWalkRetainedResult>;
        (input: SitemapWalkInput, options?: SitemapWalkOptions): Promise<SitemapWalkResult>;
    };
}

export type { SitemapDocumentLoader as S, SitemapDocumentLoadResult as a, SitemapLoadRequest as b, SitemapReaderOptions as c, SitemapReader as d, SitemapLoadFailureCode as e, SitemapLoadSource as f, SitemapReadOptions as g, SitemapReadResult as h, SitemapTargetAuthorization as i, SitemapTargetAuthorizer as j, SitemapWalkDocument as k, SitemapWalkDocumentVisitor as l, SitemapWalkEntry as m, SitemapWalkFailure as n, SitemapWalkInput as o, SitemapWalkNonRetainedResult as p, SitemapWalkOptions as q, SitemapWalkPartialReason as r, SitemapWalkResult as s, SitemapWalkRetainedResult as t };
