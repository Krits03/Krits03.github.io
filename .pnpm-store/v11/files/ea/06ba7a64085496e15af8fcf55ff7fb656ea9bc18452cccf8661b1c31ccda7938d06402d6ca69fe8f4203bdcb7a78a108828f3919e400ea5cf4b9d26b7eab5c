import type { MaybeRef } from 'vue';
import type { RobotsValue } from '../../types.js';
/**
 * Reactive robot directive value type
 */
export type ReactiveRobotsValue = MaybeRef<RobotsValue>;
/**
 * Get and set the current robots rule.
 * Supports standard directives (index, noindex, follow, nofollow) and
 * non-standard directives like noai and noimageai.
 */
export declare function useRobotsRule(rule?: ReactiveRobotsValue): import("vue").Ref<string | boolean | {
    enabled?: boolean | undefined;
    disabled?: boolean | undefined;
    index?: boolean | undefined;
    noindex?: boolean | undefined;
    follow?: boolean | undefined;
    nofollow?: boolean | undefined;
    none?: boolean | undefined;
    all?: boolean | undefined;
    noai?: boolean | undefined;
    noimageai?: boolean | undefined;
    'max-image-preview'?: "none" | "standard" | "large" | undefined;
    'max-snippet'?: number | undefined;
    'max-video-preview'?: number | undefined;
}, RobotsValue | {
    enabled?: boolean | undefined;
    disabled?: boolean | undefined;
    index?: boolean | undefined;
    noindex?: boolean | undefined;
    follow?: boolean | undefined;
    nofollow?: boolean | undefined;
    none?: boolean | undefined;
    all?: boolean | undefined;
    noai?: boolean | undefined;
    noimageai?: boolean | undefined;
    'max-image-preview'?: "none" | "standard" | "large" | undefined;
    'max-snippet'?: number | undefined;
    'max-video-preview'?: number | undefined;
}> | import("vue").WritableComputedRef<RobotsValue | undefined, RobotsValue | undefined>;
