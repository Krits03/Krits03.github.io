import { logger } from "../../logger.js";
import { defineOgImage } from "./defineOgImage.js";
export function defineOgImageComponent(component, props = {}, options = {}) {
  if (import.meta.dev) {
    logger.warn("`defineOgImageComponent()` is deprecated. Use `defineOgImage()` instead. Run `npx nuxt-og-image migrate v6` to auto-migrate.");
  }
  return defineOgImage(component, props, options);
}
