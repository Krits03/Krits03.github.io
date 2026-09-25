import type { VNode } from '../../types.js';
/** Parse a CSS unicode-range string (e.g. "U+0900-097F, U+0980-09FF") into codepoint ranges */
export declare function parseUnicodeRange(range: string): [number, number][] | null;
/** Test whether any codepoint in the set falls within the given ranges */
export declare function codepointsIntersectRanges(codepoints: Set<number>, ranges: [number, number][]): boolean;
/**
 * Extract all codepoints from text content in a node tree.
 * Works with both satori VNodes (text in props.children) and takumi nodes (text in .text field).
 */
export declare function extractCodepoints(node: VNode | Record<string, any>): Set<number>;
