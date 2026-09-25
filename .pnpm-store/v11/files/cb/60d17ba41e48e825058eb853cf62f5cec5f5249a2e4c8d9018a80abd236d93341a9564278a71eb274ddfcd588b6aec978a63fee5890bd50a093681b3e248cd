import { type InferModifiers } from '../utils/index.js';
declare const operationsGenerator: (modifiers: Partial<Record<string, string | number | boolean>>) => string;
interface UmbracoImageOptions {
    baseURL?: string;
    modifiers?: InferModifiers<typeof operationsGenerator> & {
        fit?: 'boxpad' | 'crop' | 'manual' | 'max' | 'min' | 'pad' | 'stretch' | 'contain' | 'cover';
    } & {
        sampler?: 'bicubic' | 'nearest' | 'box' | 'mitchell' | 'catmull' | 'lanczos2' | 'lanczos3' | 'lanczos5' | 'lanczos8' | 'welch' | 'robidoux' | 'robidouxsharp' | 'spline' | 'triangle' | 'hermite';
    } & {
        anchorPosition?: 'bottom' | 'bottomleft' | 'bottomright' | 'center' | 'left' | 'right' | 'top' | 'topleft' | 'topright';
    };
}
declare const _default: () => import("../../module.js").ImageProvider<UmbracoImageOptions>;
export default _default;
