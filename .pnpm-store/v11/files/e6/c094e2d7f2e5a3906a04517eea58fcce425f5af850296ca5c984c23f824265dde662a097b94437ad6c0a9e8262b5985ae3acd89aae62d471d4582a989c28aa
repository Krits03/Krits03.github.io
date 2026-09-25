import type { OgImageComponents } from '#og-image/components';
import type { OgImageOptions, ReactiveComponentProps } from '../../types.js';
type OgImageComponentOptions<T extends keyof OgImageComponents> = OgImageOptions & {
    props?: ReactiveComponentProps<OgImageComponents[T]>;
};
/**
 * Define an OG image using a component.
 *
 * @param component - The component name (must match an OgImage component)
 * @param propsOrOptions - Either component props, or an array of options for multiple images
 * @param options - Additional OG image options (width, height, etc.), or an array of options for multiple images sharing the same props
 */
export declare function defineOgImage<T extends keyof OgImageComponents>(component: T, propsOrOptions?: ReactiveComponentProps<OgImageComponents[T]> | OgImageComponentOptions<T>[], options?: OgImageOptions | OgImageComponentOptions<T>[]): string[];
export {};
