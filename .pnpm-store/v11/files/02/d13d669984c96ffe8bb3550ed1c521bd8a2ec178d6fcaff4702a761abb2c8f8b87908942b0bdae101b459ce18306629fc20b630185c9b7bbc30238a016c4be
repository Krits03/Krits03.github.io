import type { RouteLocationNormalizedLoaded } from 'vue-router';
import type { DefineOgImageInput } from '../types.js';
/**
 * Client-side processing for SPA navigations: registers a `useHead` entry pointing
 * at the correct og:image URL for the current route so iOS share sheet, devtools
 * and any other DOM reader see the current page's image instead of the initial
 * page's (#567).
 *
 * Strategy by deployment:
 *  - SSR (any flavour): point at the `/_og/r/<path>` resolver. Re-fetches the
 *    target page server-side and redirects to whatever og:image SSR emits, so the
 *    client URL always matches the server's (including useSeoMeta-injected titles
 *    and strict HMAC-signed URLs, without exposing the secret).
 *  - Pure SSG (no runtime server): rebuild the URL directly from defaults. If the
 *    page relies on useSeoMeta auto-injection the rebuilt URL won't include those
 *    values; the resolver can't help without a server.
 */
export declare function clientProcessOgImageOptions(input: DefineOgImageInput | DefineOgImageInput[], route: RouteLocationNormalizedLoaded, basePath: string): string[];
