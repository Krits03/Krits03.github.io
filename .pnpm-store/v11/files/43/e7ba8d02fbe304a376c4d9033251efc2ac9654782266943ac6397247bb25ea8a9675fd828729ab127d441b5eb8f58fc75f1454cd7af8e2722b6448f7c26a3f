import type { ImageModifiers } from '@nuxt/image';
export interface CloudflareImagesModifiers extends ImageModifiers {
    dpr: number;
    gravity: 'auto' | 'face' | 'left' | 'right' | 'top' | 'bottom' | string;
    sharpen: number;
    rotate: 90 | 180 | 270;
    brightness: number;
    contrast: number;
    gamma: number;
    saturation: number;
    anim: 'true' | 'false';
    metadata: 'copyright' | 'keep' | 'none';
    onerror: 'redirect';
    compression: 'fast';
    flip: 'h' | 'v' | 'hv';
    zoom: number;
    segment: 'foreground';
    /**
     * The variant of the image to deliver (e.g., 'public', 'thumbnail', etc.)
     * This gets priority over other modifiers.
     * @default 'public' if no modifiers is provided
     * @see https://developers.cloudflare.com/images/manage-images/create-variants/
     */
    variant: string;
}
export interface CloudflareImagesOptions {
    baseURL?: string;
    accountHash: string;
    modifiers?: Partial<CloudflareImagesModifiers>;
}
declare const _default: () => import("../../module.js").ImageProvider<CloudflareImagesOptions>;
export default _default;
