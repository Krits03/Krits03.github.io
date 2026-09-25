import type { ImageModifiers } from '@nuxt/image';
interface EdgeOnePagesModifiers extends ImageModifiers {
    /** Regular crop: '<width>x<height>' e.g. '300x400' */
    crop: string;
    /** Crop/scale gravity: center, north, south, west, east, northwest, northeast, southwest, southeast */
    gravity: string;
    /** Crop X offset */
    dx: number;
    /** Crop Y offset */
    dy: number;
    /** Inscribed circle crop radius */
    iradius: number;
    /** Smart face crop: '<width>x<height>' */
    scrop: string;
    /** Clockwise rotation angle 0-360 */
    rotate: number;
    /** Auto-rotate based on EXIF orientation */
    autoOrient: boolean;
    /** Sharpen intensity */
    sharpen: number;
    /** Strip EXIF metadata */
    strip: boolean;
    /** Progressive display (JPEG/GIF) */
    interlace: boolean | number;
    /** Pad mode (used with thumbnail + background) 0 or 1 */
    pad: boolean | number;
}
/** Options for the EdgeOne Pages image provider. */
export interface EdgeOnePagesOptions {
    /** Base URL of the EdgeOne Pages site (e.g. `https://domain`). */
    baseURL: string;
    /** Optional image processing modifiers. */
    modifiers?: Partial<EdgeOnePagesModifiers>;
}
/**
 * EdgeOne Pages image provider.
 *
 * Transforms images via the `imageMogr2` API, supporting resize,
 * crop, rotate, blur, quality, format conversion and more.
 *
 * @see https://edgeone.ai/document/162498
 */
declare const _default: () => import("../../module.js").ImageProvider<EdgeOnePagesOptions>;
export default _default;
