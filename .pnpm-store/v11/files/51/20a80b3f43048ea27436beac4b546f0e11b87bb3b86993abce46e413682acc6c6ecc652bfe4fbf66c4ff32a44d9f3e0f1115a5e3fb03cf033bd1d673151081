import { createError } from "#nuxtseo/h3";
import { createBrowser } from "#og-image/bindings/browser";
import { createScreenshot } from "./screenshot.js";
const BrowserRenderer = {
  name: "browser",
  supportedFormats: ["png", "jpeg", "jpg"],
  async debug() {
    return {};
  },
  async createImage(ctx) {
    const browser = await createBrowser(ctx.e);
    const screenshot = await createScreenshot(ctx, browser).catch((e) => e);
    await browser.close();
    if (screenshot instanceof Error) {
      return createError({
        statusCode: 400,
        cause: screenshot,
        statusMessage: `[Nuxt OG Image] Failed to create screenshot ${screenshot.message}.`
      });
    }
    return screenshot;
  }
};
export default BrowserRenderer;
