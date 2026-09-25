import type { ImageModifiers } from '@nuxt/image';
export type ImgproxyResizingType = 'fit' | 'fill' | 'fill-down' | 'force' | 'auto';
export type ImgproxyGravityType = 'ce' | 'no' | 'so' | 'ea' | 'we' | 'noea' | 'nowe' | 'soea' | 'sowe';
export interface ImgproxyCrop {
    width: number;
    height: number;
    gravity?: ImgproxyGravityType;
}
export type ImgproxyFormat = 'webp' | 'png' | 'jpg' | 'jpeg' | 'jxl' | 'avif' | 'gif' | 'ico' | 'svg' | 'heic' | 'bmp' | 'tiff' | 'pdf' | 'psd' | 'mp4';
export type ImgproxyBooleanPrimitive = string | number | boolean;
export interface ImgproxyModifiers extends Omit<ImageModifiers, 'fit' | 'format' | 'background' | 'resize' | 'width' | 'height'> {
    width: number;
    height: number;
    format: ImgproxyFormat;
    fit: 'cover' | 'contain' | 'fill' | 'inside' | 'outside';
    resizingType: ImgproxyResizingType;
    resize: string;
    size: string;
    minWidth: number;
    minHeight: number;
    zoom: string | number;
    dpr: number;
    enlarge: boolean;
    extend: boolean;
    extendAspectRatio: string;
    gravity: ImgproxyGravityType | string;
    crop: ImgproxyCrop;
    autoRotate: boolean;
    rotate: number;
    background: string;
    sharpen: number;
    pixelate: number;
    stripMetadata: boolean;
    keepCopyright: boolean;
    stripColorProfile: boolean;
    enforceThumbnail: boolean;
    maxBytes: number;
    raw: boolean;
    cachebuster: string;
    expires: number;
    filename: string;
    returnAttachment: boolean;
    preset: string;
    maxSrcResolution: number;
    maxSrcFileSize: number;
    maxAnimationFrames: number;
    maxAnimationFrameResolution: string;
    maxResultDimension: string;
}
interface ImgproxyOptions {
    baseURL: string;
    /**
     * Hex-encoded signing key. When omitted (along with `salt`), URLs are
     * generated unsigned with the `unsafe` signature segment.
     */
    key?: string;
    /** Hex-encoded signing salt. */
    salt?: string;
    modifiers?: Partial<ImgproxyModifiers>;
}
/**
 * Imgproxy provider
 * @see https://imgproxy.net/
 */
declare const _default: () => import("../../module.js").ImageProvider<ImgproxyOptions>;
export default _default;
