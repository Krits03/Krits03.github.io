interface FlyimgOptions {
    /**
     * Base URL of the Flyimg server.
     *
     * For the official Flyimg SaaS each instance gets a unique subdomain:
     * `https://img-abc123.flyimg.io`
     *
     * For self-hosted instances use the URL of your deployment,
     * e.g. `https://images.example.com`.
     */
    baseURL: string;
    /**
     * Public base URL of your website.
     *
     * Only applied to **relative** image paths (e.g. `/images/photo.jpg`) —
     * the value is prepended to produce an absolute URL that Flyimg can fetch.
     * Absolute `src` values (e.g. from a CDN) are passed through unchanged and
     * this option has no effect for those.
     *
     * Example: `https://www.example.com`
     */
    sourceURL?: string;
    /**
     * Flyimg process type.
     *
     * - `upload` (default): fetch, transform, cache and serve the image.
     * - `path`: same as upload but returns the path to the cached image as a
     *   plain-text response body instead of serving the image directly.
     *
     * @default 'upload'
     */
    processType?: 'upload' | 'path';
}
declare const _default: () => import("../../module.js").ImageProvider<FlyimgOptions>;
export default _default;
