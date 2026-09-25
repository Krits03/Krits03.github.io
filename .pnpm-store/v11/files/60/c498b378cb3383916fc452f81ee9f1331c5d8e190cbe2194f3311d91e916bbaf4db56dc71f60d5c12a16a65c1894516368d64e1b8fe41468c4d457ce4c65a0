import type { ImgHTMLAttributes } from 'vue';
import type { BaseImageProps } from '../utils/props.js';
import type { ProviderDefaults, ConfiguredImageProviders } from '@nuxt/image';
export interface ImageProps<Provider extends keyof ConfiguredImageProviders> extends BaseImageProps<Provider> {
    custom?: boolean;
    placeholder?: boolean | string | number | [w: number, h: number, q?: number, b?: number];
    placeholderClass?: string;
}
export interface DefaultSlotProps {
    imgAttrs: ImgHTMLAttributes;
    isLoaded: boolean;
    src?: string;
}
declare const _default: typeof __VLS_export;
export default _default;
declare const __VLS_export: <Provider extends keyof ConfiguredImageProviders = ProviderDefaults["provider"]>(__VLS_props: NonNullable<Awaited<typeof __VLS_setup>>["props"], __VLS_ctx?: __VLS_PrettifyLocal<Pick<NonNullable<Awaited<typeof __VLS_setup>>, "attrs" | "emit" | "slots">>, __VLS_exposed?: NonNullable<Awaited<typeof __VLS_setup>>["expose"], __VLS_setup?: Promise<{
    props: import("vue").PublicProps & __VLS_PrettifyLocal<ImageProps<Provider> & {
        onError?: ((payload: string | Event) => any) | undefined;
        onLoad?: ((payload: Event) => any) | undefined;
    }> & (typeof globalThis extends {
        __VLS_PROPS_FALLBACK: infer P;
    } ? P : {});
    expose: (exposed: import("vue").ShallowUnwrapRef<{
        imgEl: Readonly<import("vue").ShallowRef<HTMLImageElement | null, HTMLImageElement | null>>;
    }>) => void;
    attrs: any;
    slots: {
        default(props: DefaultSlotProps): any;
    };
    emit: {
        (event: "load", payload: Event): unknown;
        (event: "error", payload: string | Event): unknown;
    };
}>) => import("vue").VNode & {
    __ctx?: NonNullable<Awaited<typeof __VLS_setup>>;
};
type __VLS_PrettifyLocal<T> = (T extends any ? {
    [K in keyof T]: T[K];
} : {
    [K in keyof T as K]: T[K];
}) & {};
