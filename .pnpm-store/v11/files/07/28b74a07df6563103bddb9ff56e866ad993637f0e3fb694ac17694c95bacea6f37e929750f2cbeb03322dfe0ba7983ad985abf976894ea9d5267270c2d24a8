import type { ImgHTMLAttributes } from 'vue';
import type { BaseImageProps } from '../utils/props.js';
import type { DataAttributes } from '../types.js';
import type { ConfiguredImageProviders, ProviderDefaults } from '@nuxt/image';
export interface PictureProps<Provider extends keyof ConfiguredImageProviders> extends BaseImageProps<Provider> {
    legacyFormat?: string;
    imgAttrs?: ImgHTMLAttributes & DataAttributes;
}
declare const __VLS_export: <Provider extends keyof ConfiguredImageProviders = ProviderDefaults["provider"]>(__VLS_props: NonNullable<Awaited<typeof __VLS_setup>>["props"], __VLS_ctx?: __VLS_PrettifyLocal<Pick<NonNullable<Awaited<typeof __VLS_setup>>, "attrs" | "emit" | "slots">>, __VLS_exposed?: NonNullable<Awaited<typeof __VLS_setup>>["expose"], __VLS_setup?: Promise<{
    props: import("vue").PublicProps & __VLS_PrettifyLocal<PictureProps<Provider> & {
        onError?: ((payload: string | Event) => any) | undefined;
        onLoad?: ((payload: Event) => any) | undefined;
    }> & (typeof globalThis extends {
        __VLS_PROPS_FALLBACK: infer P;
    } ? P : {});
    expose: (exposed: {}) => void;
    attrs: any;
    slots: {};
    emit: {
        (event: "load", payload: Event): unknown;
        (event: "error", payload: string | Event): unknown;
    };
}>) => import("vue").VNode & {
    __ctx?: NonNullable<Awaited<typeof __VLS_setup>>;
};
declare const _default: typeof __VLS_export;
export default _default;
type __VLS_PrettifyLocal<T> = (T extends any ? {
    [K in keyof T]: T[K];
} : {
    [K in keyof T as K]: T[K];
}) & {};
