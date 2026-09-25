export declare const DEFAULT_XML_STREAM_CHUNK_SIZE: number;
export type SitemapCompressionEncoding = 'gzip' | 'deflate';
interface NodeResponseWritable {
    once: (event: 'drain', listener: () => void) => unknown;
    write: (chunk: Uint8Array) => boolean;
}
export interface NodeResponseStream {
    abort: (reason?: unknown) => void;
    on: {
        (event: 'end', listener: () => void): NodeResponseStream;
        (event: 'error', listener: (error: unknown) => void): NodeResponseStream;
    };
    pipe: (destination: NodeResponseWritable) => NodeResponseWritable;
}
export declare function isReadableStream(value: unknown): value is ReadableStream<Uint8Array>;
export declare function hasNonIdentityEncoding(value: unknown): boolean;
/**
 * Adapt a Web stream to the small Node stream surface H3 consumes. H3 v1 writes
 * Web streams without waiting for `drain`; this adapter keeps production Node
 * responses pull-driven and forwards disconnects to the Web stream's `cancel()`.
 */
export declare function createNodeResponseStream(source: ReadableStream<Uint8Array>, onCancelError: (error: unknown) => void): NodeResponseStream;
/**
 * Convert synchronous XML fragments into a pull-driven byte stream. Fragments are
 * batched so large sitemaps do not enqueue one tiny chunk per URL.
 */
export declare function createChunkedXmlStream(chunks: Iterable<string>, targetChunkSize?: number): ReadableStream<Uint8Array>;
/** Select the best compression format supported by CompressionStream. */
export declare function negotiateCompressionEncoding(acceptEncoding: string): SitemapCompressionEncoding | null;
export {};
