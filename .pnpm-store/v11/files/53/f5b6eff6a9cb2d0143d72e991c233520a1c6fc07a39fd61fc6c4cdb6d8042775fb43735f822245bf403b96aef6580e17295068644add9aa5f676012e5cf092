type SitemapChunk = string | Uint8Array;
type SitemapInput = SitemapChunk | Iterable<SitemapChunk> | AsyncIterable<SitemapChunk> | ReadableStream<SitemapChunk>;
type SitemapFormat = 'xml' | 'rss2' | 'atom1' | 'text';
type SitemapDocumentKind = 'urlset' | 'index';
interface SitemapAlternative {
    rel?: string;
    hreflang?: string;
    href: string;
}
interface SitemapImage {
    loc: string;
    caption?: string;
    geoLocation?: string;
    title?: string;
    license?: string;
}
interface SitemapMediaContent {
    url: string;
    type?: string;
    medium?: string;
}
interface SitemapMediaThumbnail {
    url: string;
    width?: string;
    height?: string;
}
interface SitemapExtensions {
    alternatives?: SitemapAlternative[];
    images?: SitemapImage[];
    videos?: Record<string, unknown>[];
    news?: Record<string, unknown>;
    media?: {
        contents?: SitemapMediaContent[];
        thumbnails?: SitemapMediaThumbnail[];
    };
}
interface SitemapUrlRecord {
    loc: string;
    lastmod?: string;
    changefreq?: string;
    priority?: string;
    extensions?: SitemapExtensions;
}
interface SitemapReference {
    loc: string;
    lastmod?: string;
}
interface SitemapUrlsetDocument {
    _tag: 'urlset';
    format: Exclude<SitemapFormat, never>;
    entries: SitemapUrlRecord[];
}
interface SitemapIndexDocument {
    _tag: 'index';
    format: 'xml';
    entries: SitemapReference[];
}
type SitemapDocument = SitemapUrlsetDocument | SitemapIndexDocument;
type SitemapIssueCode = 'decoded_limit' | 'entry_limit' | 'empty' | 'html' | 'invalid_utf8' | 'malformed' | 'unsupported' | 'missing_loc' | 'invalid_loc';
interface SitemapIssue {
    code: SitemapIssueCode;
    severity: 'warning' | 'error';
    message: string;
    entryIndex?: number;
    field?: string;
    value?: unknown;
}
type SitemapCompleteness = {
    _tag: 'complete';
} | {
    _tag: 'partial';
    reason: 'decoded_limit' | 'entry_limit';
} | {
    _tag: 'failed';
    reason: 'empty' | 'html' | 'unsupported' | 'invalid_utf8' | 'malformed';
};
interface SitemapParseSummary {
    bytesRead: number;
    entriesRead: number;
    compressed: boolean;
}
type SitemapParseEvent = {
    _tag: 'document';
    format: SitemapFormat;
    kind: SitemapDocumentKind;
} | {
    _tag: 'url';
    entry: SitemapUrlRecord;
} | {
    _tag: 'sitemap';
    entry: SitemapReference;
} | {
    _tag: 'issue';
    issue: SitemapIssue;
} | {
    _tag: 'end';
    completeness: SitemapCompleteness;
    summary: SitemapParseSummary;
};
interface ParseSitemapOptions {
    formatHint?: 'text';
    maxDecodedBytes?: number;
    maxEntries?: number;
    maxEntryBytes?: number;
}
type CollectSitemapResult = {
    _tag: 'document';
    document: SitemapDocument;
    issues: SitemapIssue[];
    completeness: Extract<SitemapCompleteness, {
        _tag: 'complete' | 'partial';
    }>;
    summary: SitemapParseSummary;
} | {
    _tag: 'partial';
    issues: SitemapIssue[];
    completeness: Extract<SitemapCompleteness, {
        _tag: 'partial';
    }>;
    summary: SitemapParseSummary;
} | {
    _tag: 'failure';
    issues: SitemapIssue[];
    completeness: Extract<SitemapCompleteness, {
        _tag: 'failed';
    }>;
    summary: SitemapParseSummary;
};

export type { CollectSitemapResult as C, ParseSitemapOptions as P, SitemapReference as S, SitemapCompleteness as a, SitemapDocument as b, SitemapDocumentKind as c, SitemapExtensions as d, SitemapFormat as e, SitemapInput as f, SitemapIssue as g, SitemapIssueCode as h, SitemapUrlRecord as i, SitemapParseEvent as j, SitemapAlternative as k, SitemapChunk as l, SitemapImage as m, SitemapIndexDocument as n, SitemapMediaContent as o, SitemapMediaThumbnail as p, SitemapParseSummary as q, SitemapUrlsetDocument as r };
