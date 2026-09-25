import type { OgImageIconsData, OgImageRenderEventContext } from '../../../../../types.js';
declare module '#og-image-virtual/iconify-json-icons.mjs' {
    function loadIcons(): Promise<OgImageIconsData>;
}
/**
 * Service function to get emoji SVGs from local iconify JSON files
 * This does not perform HTML replacement - that's handled by the AST plugin
 * This implementation prioritizes local deps over API calls (addresses issue #354)
 * Icons are loaded lazily on first use to avoid 24MB+ memory at startup
 */
export declare function getEmojiSvg(ctx: OgImageRenderEventContext, emojiChar: string): Promise<string | null>;
