import { withBase } from "ufo";
import { useRuntimeConfig } from "#nuxtseo/nitro";
import { getSiteConfig } from "#site-config/server/composables";
import { getCloudflareAssets } from "../../../util/cloudflareAssets.js";
import { fetchLocalAsset } from "../../../util/fetchLocalAsset.js";
import { getFetchTimeout } from "../../../util/fetchTimeout.js";
import { useOgImageRuntimeConfig } from "../../../utils.js";
import { fetchSpecialFontUrl, isDataFontUrl, isExternalFontUrl } from "./external-url.js";
export async function resolve(event, font) {
  const path = font.src || font.localPath;
  const runtimeConfig = useOgImageRuntimeConfig();
  const timeout = getFetchTimeout(runtimeConfig);
  const { app } = useRuntimeConfig();
  const fullPath = withBase(path, app.baseURL);
  if (path && (isDataFontUrl(path) || isExternalFontUrl(path)))
    return fetchSpecialFontUrl(path, getSiteConfig(event).url, timeout);
  const ab = await fetchLocalAsset(event, fullPath, { fetchTimeout: timeout });
  if (ab)
    return Buffer.from(ab);
  if (!getCloudflareAssets(event) && !event.context._ogImageWarnedMissingAssets) {
    event.context._ogImageWarnedMissingAssets = true;
    console.warn(
      `[Nuxt OG Image] No ASSETS binding found on Cloudflare Workers. Font loading will fail. To fix this, add \`nitro: { cloudflare: { deployConfig: true } }\` to your nuxt.config and deploy with \`npx wrangler --cwd .output deploy\` instead of using the --assets flag.`
    );
  }
  throw new Error(`[Nuxt OG Image] Cannot resolve font "${font.family}" on Cloudflare Workers: no ASSETS binding available (path: ${fullPath}).`);
}
