import { useRuntimeConfig } from "nuxt/app";
import { logger } from "../../logger.js";
export function defineOgImage(_component, _props = {}, _options = {}) {
  if (import.meta.dev) {
    logger.warn("`defineOgImage()` is skipped as the OG Image module is not enabled.");
  }
}
export function defineOgImageComponent(_component, _props = {}, _options = {}) {
  if (import.meta.dev) {
    logger.warn("`defineOgImageComponent()` is deprecated. Use `defineOgImage()` instead. Run `npx nuxt-og-image migrate v6` to auto-migrate.");
  }
}
export function defineOgImageScreenshot(_options = {}) {
  if (import.meta.dev) {
    if (useRuntimeConfig()["nuxt-og-image"]) {
      console.warn("`defineOgImageScreenshot()` is skipped as the `browser` compatibility is disabled.");
    } else {
      console.warn("`defineOgImageScreenshot()` is skipped as the OG Image module is not enabled.");
    }
  }
}
