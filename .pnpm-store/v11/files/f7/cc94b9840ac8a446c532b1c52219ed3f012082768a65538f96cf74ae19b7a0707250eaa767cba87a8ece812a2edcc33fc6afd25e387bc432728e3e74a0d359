import type { HTTPStorageOptions, NodeFSSOptions, IPXOptions as CoreIPXOptions, IPXModifiers } from 'ipx';
export type { IPXModifiers };
export interface IPXRuntimeConfig extends Omit<CoreIPXOptions, 'storage' | 'httpStorage'> {
    http: HTTPStorageOptions;
    fs: NodeFSSOptions;
    baseURL: string;
}
export interface IPXOptions extends Omit<IPXRuntimeConfig, 'alias'> {
    modifiers: Partial<IPXModifiers>;
}
export declare const operationsGenerator: (modifiers: Partial<Record<string, string | number | boolean>>) => string;
declare const _default: () => import("../../module.js").ImageProvider<Partial<IPXOptions>>;
export default _default;
