import type { Storage } from 'unstorage';
import type { OgImageOptions, RuntimeFontConfig } from '../../../types.js';
export declare const htmlPayloadCache: Storage<{
    expiresAt: number;
    value: OgImageOptions;
}>;
export declare const prerenderOptionsCache: Storage<OgImageOptions | [string, OgImageOptions][]> | undefined;
export declare const emojiCache: Storage<string>;
declare class BoundedMap<V> {
    private max;
    private map;
    constructor(max: number);
    get(key: string): V | undefined;
    set(key: string, value: V): void;
}
export declare const fontCache: BoundedMap<BufferSource>;
export declare const fontArrayCache: BoundedMap<RuntimeFontConfig[]>;
export {};
