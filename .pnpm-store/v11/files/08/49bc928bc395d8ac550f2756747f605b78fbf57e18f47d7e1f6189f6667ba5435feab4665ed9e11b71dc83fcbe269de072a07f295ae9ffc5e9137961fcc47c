import { ImageMeta } from "./_chunks/libs/image-meta.mjs";
import { HTTPError } from "./_chunks/libs/h3.mjs";
import { NodeHttpHandler, Server, ServerOptions } from "srvx";
import { Color, KernelEnum, Sharp, SharpOptions } from "sharp";
import { Config } from "svgo";
import { Driver, Storage } from "unstorage";
interface HandlerContext {
  /**
   * Optional quality setting for the output image, affects compression in certain formats.
   * @optional
   */
  quality?: number;
  /**
   * Specifies the method to fit the image to the dimensions provided, e.g., 'contain', 'cover'.
   * @optional
   */
  fit?: "contain" | "cover" | "fill" | "inside" | "outside";
  /**
   * The position used for cropping or positioning, specified as a number or string.
   * @optional
   */
  position?: number | string;
  /**
   * Background colour to be used if necessary, provided as a colour object. See {@link Color}.
   * @optional
   */
  background?: Color;
  /**
   * Specifies whether to enlarge the image if it is smaller than the desired size.
   * @optional
   */
  enlarge?: boolean;
  /**
   * The type of kernel to use for image operations such as resizing. See {@link KernelEnum}.
   * @optional
   */
  kernel?: keyof KernelEnum;
  /**
   * The maximum width and height of the output image, or `false` when
   * unlimited. Set from the `maxOutputDimension` IPX option.
   * @optional
   */
  maxOutputDimension?: number | false;
  /**
   * Dimensions the image is expected to have once the resize modifiers
   * (`resize`, `width`, `height`) have been applied, recorded by those
   * handlers after their own clamping.
   *
   * libvips resizes before it extends, whatever order the modifiers appear in
   * the URL, so `extend` budgets its edges against these rather than against
   * {@link meta}: budgeting against the source lets the two clamps stack and
   * the canvas end up at twice `maxOutputDimension` on each axis.
   *
   * Undefined when no resize modifier was applied (or when nothing could be
   * projected from it), in which case `extend` falls back to {@link meta}.
   * @optional
   */
  outputDimensions?: {
    width?: number;
    height?: number;
  };
  /**
   * Metadata about the image being processed.
   */
  meta: ImageMeta;
}
interface Handler {
  /**
   * An array of functions that convert the given string arguments into usable forms.
   */
  args: ((argument: string) => any)[];
  /**
   * Defines the order in which this handler should be applied relative to other handlers.
   * @optional
   */
  order?: number;
  /**
   * Function to apply the effects of this handler to the image pipeline.
   * @param {HandlerContext} context - The current image processing context. See {@link HandlerContext}.
   * @param {Sharp} pipe - The Sharp instance to use for image processing. See {@link Sharp}.
   * @param {...any} arguments_ - Transformed arguments to use in the handler.
   */
  apply: (context: HandlerContext, pipe: Sharp, ...arguments_: any[]) => any;
}
type IPXStorageMeta = {
  /**
   * The modification time of the stored item.
   * @optional
   */
  mtime?: Date | number | string;
  /**
   * The maximum age (in seconds) at which the stored item should be considered fresh.
   * @optional
   */
  maxAge?: number | string;
};
/**
 * Options specific to image saving operations.
 */
type IPXStorageOptions = Record<string, unknown>;
type MaybePromise<T> = T | Promise<T>;
interface IPXStorage {
  /**
   * A descriptive name for the storage type.
   */
  name: string;
  /**
   * Retrieves metadata for an image identified by 'id'.
   * @param {string} id - The identifier for the image.
   * @param {IPXStorageOptions} [opts] - Optional metadata retrieval options. See {@link IPXStorageOptions}.
   * @returns {MaybePromise<IPXStorageMeta | undefined>} A promise or direct return of the metadata, or undefined if not found. See {@link IPXStorageMeta}.
   */
  getMeta: (id: string, opts?: IPXStorageOptions) => MaybePromise<IPXStorageMeta | undefined>;
  /**
   * Get the actual data for an image identified by 'id'.
   * @param {string} id - The identifier for the image.
   * @param {IPXStorageOptions} [opts] - Optional options for the data retrieval. See {@link IPXStorageOptions}.
   * @returns {MaybePromise<Buffer | ArrayBuffer | undefined>} A promise or direct return of the image data as an ArrayBuffer, or undefined if not found. See {@link ArrayBuffer}.
   */
  getData: (id: string, opts?: IPXStorageOptions) => MaybePromise<Buffer | ArrayBuffer | undefined>;
}
type IPXSourceMeta = {
  /**
   * The modification time of the source. Used for cache validation.
   * @optional
   */
  mtime?: Date;
  /**
   * The maximum age (in seconds) that the source should be considered fresh.
   * @optional
   */
  maxAge?: number;
};
type FlagModifier = true | "true" | "";
type FormatModifier = "jpeg" | "jpg" | "png" | "webp" | "avif" | "gif" | "heif" | "tiff" | "auto" | (string & {});
interface IPXModifiers {
  format: FormatModifier;
  f: FormatModifier;
  fit: "contain" | "cover" | "fill" | "inside" | "outside" | (string & {});
  resize: string;
  s: string;
  quality: number | string;
  q: number | string;
  background: string;
  b: string;
  position: string;
  pos: string;
  enlarge: FlagModifier;
  kernel: "nearest" | "cubic" | "mitchell" | "lanczos2" | "lanczos3" | (string & {});
  trim: number | string;
  extend: string;
  extract: string;
  crop: string;
  rotate: number | string;
  autoorient: FlagModifier;
  flip: FlagModifier;
  flop: FlagModifier;
  sharpen: number | string;
  median: number | string;
  blur: number | string;
  dilate: number | string;
  erode: number | string;
  clahe: number | string;
  flatten: FlagModifier;
  unflatten: FlagModifier;
  gamma: string;
  negate: FlagModifier | string;
  normalize: FlagModifier | string;
  threshold: number | string;
  linear: string;
  modulate: string;
  brightness: number | string;
  saturation: number | string;
  hue: number | string;
  lightness: number | string;
  opacity: number | string;
  tint: number | string;
  grayscale: FlagModifier;
  animated: FlagModifier;
  a: FlagModifier;
  width: string | number;
  w: string | number;
  height: string | number;
  h: string | number;
}
/**
 * A function type that defines an IPX image processing instance.
 *
 * This function takes an image identifier and optional modifiers and request options, then provides methods to retrieve
 * image metadata and process the image according to the specified modifiers.
 *
 * @param {string} id - The identifier for the image. This can be a URL or a path, depending on the storage implementation.
 * @param {partial<Record<HandlerName | "f" | "format" | "a" | "animated", string>>} [modifiers] - Modifiers to be applied to the image,
 * such as resizing, cropping or format conversion. This record contains predefined keys such as 'f' or 'format' to specify the output to
 * specify the output image format, and 'a' or 'animated' to specify whether the image should be processed as an animation. See
 * {@link HandlerName}.
 * @param {any} [requestOptions] - Additional options that may be needed for request handling, specific to the storage backend.
 * Returns an object with methods:
 * - `getSourceMeta`: A method that returns a promise resolving to the source image metadata (`IPXSourceMeta`).
 * - `process`: A method that returns a promise resolving to an object containing the processed image data, metadata,
 * and format. The image data can be in the form of a `buffer` or a string, depending on the format and processing.
 */
type IPX = (id: string, modifiers?: Partial<IPXModifiers>, requestOptions?: any) => {
  getSourceMeta: () => Promise<IPXSourceMeta>;
  process: () => Promise<{
    data: Buffer | string;
    meta?: ImageMeta;
    format?: string;
  }>;
};
type IPXOptions = {
  /**
   * Default cache duration in seconds. If not specified, a default of 1 minute is used.
   * @optional
   */
  maxAge?: number;
  /**
   * Maximum width and height (in pixels) of the output image.
   *
   * Modifiers are user input and sharp's `limitInputPixels` only bounds the
   * *input*, so without this limit a request such as
   * `/enlarge,s_20000x20000/img.jpg` or `/extend_10000_10000_10000_10000/img.jpg`
   * makes sharp allocate a multi-gigabyte output buffer from a tiny source
   * image, which is an easy way to exhaust the server memory.
   *
   * Requested `width`, `height`, `resize` dimensions are clamped to this value
   * (preserving the requested aspect ratio) and `extend` edges are clamped so
   * that the extended canvas stays within it.
   *
   * Set to `false` to disable the limit (only safe when modifiers come from a
   * trusted source).
   *
   * @default 8192
   * @optional
   */
  maxOutputDimension?: number | false;
  /**
   * A mapping of URL aliases to their corresponding URLs, used to simplify resource identifiers.
   * @optional
   */
  alias?: Record<string, string>;
  /**
   * Configuration options for the Sharp image processing library.
   * @optional
   */
  sharpOptions?: SharpOptions;
  /**
   * Primary storage backend for handling image assets.
   */
  storage: IPXStorage;
  /**
   * An optional secondary storage backend used when images are fetched via HTTP.
   * @optional
   */
  httpStorage?: IPXStorage;
  /**
   * Options for SVG images, which are processed by SVGO instead of Sharp.
   * @optional
   */
  svg?: {
    /**
     * Configuration for the SVGO library used to optimize SVG images.
     *
     * SVGO's `preset-default` is applied unless custom `plugins` are configured.
     * Set to `false` to disable optimization. Sanitization is applied either way.
     * @optional
     */
    optimize?: false | Config;
    /**
     * Disable SVG sanitization.
     *
     * Sanitized SVG images cannot execute scripts. Only disable this if all sources
     * are fully trusted, as it allows serving SVG images with XSS payloads.
     * @default false
     * @optional
     */
    unsafeSkipSanitize?: boolean;
  };
};
/**
 * Creates an IPX image processing instance with the specified options.
 * @param {IPXOptions} userOptions - Configuration options for the IPX instance. See {@link IPXOptions}.
 * @returns {IPX} An IPX processing function configured with the given options. See {@link IPX}.
 * @throws {Error} If critical options such as storage are missing or incorrectly configured.
 */
declare function createIPX(userOptions: IPXOptions): IPX;
type FetchHandler = (request: Request | string | URL) => Response | Promise<Response>;
interface IPXHandlerOptions {
  /**
   * Custom URL parser to extract the resource id and modifiers from the request URL.
   * Can be async.
   *
   * Receives the raw (absolute, still percent-encoded) request URL, so parsers can
   * decode it themselves without going through h3's normalization.
   *
   * Defaults to {@link parseIPXURL} which handles URLs in the form `/<modifiers>/<id>`.
   *
   * Returned values are escaped (control characters) by the handler, so custom parsers
   * do not need to escape them. This is not an access check: exactly as with the default
   * parser, what the resulting `id` is allowed to resolve to is enforced by the storage
   * layer. Throw an `HTTPError` to reject a request with a specific status code.
   *
   * @optional
   */
  parseURL?: IPXURLParser;
}
declare function createIPXFetchHandler(ipx: IPX, opts?: IPXHandlerOptions): FetchHandler;
declare function createIPXNodeHandler(ipx: IPX, opts?: IPXHandlerOptions): NodeHttpHandler;
declare function serveIPX(ipx: IPX, opts?: Omit<ServerOptions, "fetch"> & IPXHandlerOptions): Server;
interface IPXParsedURL {
  /**
   * The identifier of the source image (path or URL, depending on the storage).
   */
  id: string;
  /**
   * Modifiers to apply, keyed by modifier name. See {@link IPXModifiers}.
   *
   * Values are coerced to strings. Use `""` (or `undefined`) for valueless
   * modifiers such as `grayscale`.
   */
  modifiers: Record<string, string | number | boolean | undefined>;
}
type IPXURLParser = (url: string) => IPXParsedURL | Promise<IPXParsedURL>;
/**
 * Default IPX URL parser, handling URLs in the form `/<modifiers>/<id>`.
 *
 * Use `_` as the modifiers segment to apply none (`/_/image.png`).
 *
 * @param {string} url - The raw (absolute) request URL.
 * @returns {IPXParsedURL} The parsed resource id and modifiers. See {@link IPXParsedURL}.
 * @throws {HTTPError} If the modifiers segment is missing.
 */
declare function parseIPXURL(url: string): IPXParsedURL;
type HTTPStorageOptions = {
  /**
   * Custom options for fetch operations, such as headers or method overrides.
   *
   * Redirects are followed manually (one hop at a time) so that each redirect target
   * can be re-validated against the {@link HTTPStorageOptions.domains} allowlist
   * (and {@link HTTPStorageOptions.blockPrivateIPs} when enabled).
   * Explicitly setting `redirect` here opts out of this protection: the value is passed
   * to `fetch` as-is and redirect targets are **not** validated (a redirect to an
   * internal address is then possible: SSRF).
   * @optional
   */
  fetchOptions?: RequestInit;
  /**
   * Default maximum age (in seconds) for cache control. If not specified, defaults to the environment setting or 300 seconds.
   * @optional
   */
  maxAge?: number;
  /**
   * Whitelist of domains from which resource fetching is allowed. Can be a single string or an array of strings.
   *
   * Only `http:` and `https:` URLs are allowed. Redirects are followed only within this
   * allowlist (up to 3 hops): a redirect to a host that is not listed is rejected with
   * `403 IPX_FORBIDDEN_HOST`, so an allowlisted host cannot bounce IPX to an internal
   * address. Hosts that redirect to a CDN must have the CDN hostname listed here too.
   * @optional
   */
  domains?: string | string[];
  /**
   * If set to true, allows retrieval from any domain. Overrides the domain whitelist.
   * @optional
   */
  allowAllDomains?: boolean;
  /**
   * If set to true, ignore the cache control header in responses and use the default or specified maxAge.
   * @optional
   */
  ignoreCacheControl?: boolean;
  /**
   * If set to true, reject URLs whose host is (or resolves to) a non-public IP address
   * with `403 IPX_FORBIDDEN_IP`. Checked for the requested URL and for every redirect hop.
   *
   * This is **defense in depth**, not the primary access control: the
   * {@link HTTPStorageOptions.domains} allowlist is. It only helps when an allowlisted
   * (or, with `allowAllDomains`, arbitrary) hostname points at loopback, link-local
   * (`169.254.169.254`, the cloud metadata service), RFC1918, CGNAT, unique-local or
   * otherwise non-public space.
   *
   * Disabled by default because many legitimate deployments fetch from in-cluster origins
   * (internal object storage, sidecars, `localhost` during development), which this blocks.
   * @optional
   * @default false
   */
  blockPrivateIPs?: boolean;
};
/**
 * Creates an HTTP storage handler for IPX that fetches image data from external URLs.
 * This handler allows configuration to specify allowed domains, caching behaviour and custom fetch options.
 *
 * @param {HTTPStorageOptions} [_options={}] - Configuration options for HTTP storage, with defaults possibly taken from environment variables. See {@link HTTPStorageOptions}.
 * @returns {IPXStorage} An IPXStorage interface implementation for retrieving images over HTTP. See {@link IPXStorage}.
 * @throws {H3Error} If validation of the requested URL fails due to a missing hostname or denied host access. See {@link H3Error}.
 */
declare function ipxHttpStorage(_options?: HTTPStorageOptions): IPXStorage;
type NodeFSSOptions = {
  /**
   * The directory or list of directories from which to serve files. If not specified, the current directory is used by default.
   * @optional
   */
  dir?: string | string[];
  /**
   * `max-age`, in seconds, reported for files served from this storage. Used for the
   * `cache-control` header. Falls back to the IPX-wide `maxAge` (default 60) when unset.
   *
   * `0` is meaningful and is passed through as-is — it disables caching rather than
   * falling back to the default.
   * @optional
   */
  maxAge?: number;
  /**
   * If set to true, a symlink inside {@link NodeFSSOptions.dir} may resolve to a file outside
   * of it. By default such files are rejected with `403 IPX_FORBIDDEN_SYMLINK`, since the
   * lexical `../` check alone says nothing about where a path physically ends up.
   *
   * Symlinks that stay inside `dir` are always followed, whatever this is set to.
   *
   * This is **defense in depth**, not a fix for a remotely reachable hole: planting a symlink
   * in the served directory already requires a symlink-create or arbitrary-write primitive
   * there, and the served filesystem is assumed to be trusted. Comparable static file servers
   * (`express.static`, nginx with `disable_symlinks off`) follow symlinks by default too.
   *
   * Enable it for the deployments where symlinking assets into the served directory is
   * deliberate — monorepo `public/` layouts, CI artifact linking, Docker layer tricks.
   * @optional
   * @default false
   */
  allowSymlinksOutsideDir?: boolean;
};
/**
 * Creates a file system storage handler for IPX that allows images to be served from local directories specified in the options.
 * This handler resolves directories and handles file access, ensuring that files are served safely.
 *
 * @param {NodeFSSOptions} [_options={}] - File system storage configuration options, with optional directory paths and caching configuration. See {@link NodeFSSOptions}.
 * @returns {IPXStorage} An implementation of the IPXStorage interface for accessing images stored on the local file system. See {@link IPXStorage}.
 * @throws {H3Error} If there is a problem accessing the file system module or resolving/reading files. See {@link H3Error}.
 */
declare function ipxFSStorage(_options?: NodeFSSOptions): IPXStorage;
type UnstorageIPXStorageOptions = {
  /**
   * Optional prefix to be placed in front of each storage key, which can help to name or categorise stored items.
   * @optional
   */
  prefix?: string;
};
/**
 * Adapts an Unstorage driver or storage system to comply with the IPXStorage interface required by IPX.
 * This allows various Unstorage-compatible storage systems to be used to manage image data with IPX.
 *
 * @param {Storage | Driver} storage - The Unstorage driver or storage instance to adapt. See {@link Storage} and {@link Driver}.
 * @param {UnstorageIPXStorageOptions | string} [_options={}] - Configuration options for the adapter, which can be a simple string prefix or an options object. See {@link UnstorageIPXStorageOptions}.
 * @returns {IPXStorage}. An IPXStorage compliant object that implements the necessary methods to interact with the provided unstorage driver or storage system. See {@link IPXStorage}.
 * @throws {H3Error} If there is a problem retrieving or converting the storage data, detailed error information is thrown. See {@link H3Error}.
 */
declare function unstorageToIPXStorage(storage: Storage | Driver, _options?: UnstorageIPXStorageOptions | string): IPXStorage;
export { HTTPError, type HTTPStorageOptions, type Handler, type HandlerContext, type IPX, type IPXHandlerOptions, type IPXModifiers, type IPXOptions, type IPXParsedURL, type IPXStorage, type IPXStorageMeta, type IPXStorageOptions, type IPXURLParser, type NodeFSSOptions, type UnstorageIPXStorageOptions, createIPX, createIPXFetchHandler, createIPXNodeHandler, ipxFSStorage, ipxHttpStorage, parseIPXURL, serveIPX, unstorageToIPXStorage };