import type { ElementNode } from 'ultrahtml';
import type { OgImageRenderEventContext, VNode } from '../../../types.js';
import { parseStyleAttr } from './style-attr.js';
export { parseStyleAttr };
export declare const SVG_CAMEL_ATTR_VALUES: Set<string>;
/**
 * Resolve an SVG element's width or height from multiple sources:
 * 1. Numeric HTML attribute (e.g. width="24")
 * 2. Style property (e.g. style.width = 48 or "48px")
 * 3. viewBox (3rd/4th value for width/height)
 *
 * Percentage attributes are skipped (returned as undefined) so callers
 * can fall back to ancestor or renderer-specific resolution.
 */
export declare function resolveSvgDimension(props: Record<string, any>, style: Record<string, any> | undefined, key: 'width' | 'height'): number | undefined;
export declare function elementToVNode(el: ElementNode): VNode;
export declare function htmlToVNode(html: string): VNode;
export declare function warnUnsupportedSvgElements(vnode: VNode, component?: string): void;
export interface CreateVNodesOptions {
    wrapperStyle?: string;
}
export declare function createVNodes(ctx: OgImageRenderEventContext, options?: CreateVNodesOptions): Promise<VNode>;
