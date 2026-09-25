type SharpOperationMap = {
    rotate: [angle?: number, options?: {
        background: Color;
    }];
    flip: [];
    flop: [];
    sharpen: [sigma?: number] | [options?: {
        sigma?: number;
        m1?: number;
        m2?: number;
        x1?: number;
        y2?: number;
        y3?: number;
    }];
    median: [size?: number];
    blur: [sigma?: number] | [options?: {
        sigma?: number;
        precision?: 'integer' | 'float' | 'approximate';
        minAmplitude?: number;
    }];
    flatten: [options?: {
        background: Color;
    }];
    unflatten: [];
    gamma: [gamma?: number, gammaOut?: number];
    negate: [options?: {
        alpha?: boolean;
    }];
    normalize: [lower?: number, upper?: number];
    normalise: [lower?: number, upper?: number];
    clahe: [options?: {
        width: number;
        height: number;
        maxSlope?: number;
    }];
    convolve: [kernel: {
        width: number;
        height: number;
        kernel: number[];
        offset?: number;
    }];
    threshold: [value?: number, options?: {
        grayscale?: boolean;
    }];
    linear: [a?: number | number[], b?: number | number[]];
    recomb: [matrix: number[][]];
    modulate: [
        options?: {
            brightness?: number;
            saturation?: number;
            hue?: number;
            lightness?: number;
        }
    ];
    tint: [color: Color];
    grayscale: [];
    greyscale: [];
    pipelineColorspace: [colorspace: SharpColorspace];
    pipelineColourspace: [colourspace: SharpColorspace];
    toColorspace: [colorspace: SharpColorspace];
    toColourspace: [colourspace: SharpColorspace];
    removeAlpha: [];
    ensureAlpha: [alpha?: number];
    extractChannel: [channel: 'red' | 'green' | 'blue' | 'alpha'];
};
type SharpColorspace = 'srgb' | 'rgb' | 'scrgb' | 'rgb16' | 'cmyk' | 'lab' | 'b-w' | string;
type Color = string | {
    r: number;
    g: number;
    b: number;
    alpha?: number;
} | {
    h: number;
    s: number;
    l: number;
    alpha?: number;
} | {
    h: number;
    s: number;
    v: number;
    alpha?: number;
} | {
    c: number;
    m: number;
    y: number;
    k: number;
    alpha?: number;
} | {
    h: number;
    w: number;
    b: number;
} | {
    l: number;
    c: number;
    h: number;
} | {
    l: number;
    a: number;
    b: number;
} | {
    h: number;
    c: number;
    g: number;
};
type KnownSharpOperation = {
    [K in keyof SharpOperationMap]: SharpOperationMap[K] extends [] ? [K] : [K, ...SharpOperationMap[K]];
}[keyof SharpOperationMap];
type CustomSharpOperation<K extends string = string> = K extends keyof SharpOperationMap ? never : [key: K, ...args: any[]];
type SharpOperation = KnownSharpOperation | CustomSharpOperation;
type DirectusModifiers = {
    key: string;
} | {
    key?: never;
    withoutEnlargement?: boolean;
    transforms?: SharpOperation[];
};
interface DirectusOptions {
    baseURL: string;
    modifiers?: DirectusModifiers;
}
declare const _default: () => import("../../module.js").ImageProvider<DirectusOptions>;
export default _default;
