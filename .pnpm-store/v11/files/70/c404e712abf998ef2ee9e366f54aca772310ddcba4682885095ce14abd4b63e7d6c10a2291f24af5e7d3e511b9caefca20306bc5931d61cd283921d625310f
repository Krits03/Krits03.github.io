import { useNuxt, useLogger } from '@nuxt/kit';
import { useSiteConfig } from 'nuxt-site-config/kit';
import { $fetch } from 'ofetch';
import { isTest } from 'std-env';
import { detectNuxtSeoModules } from './kit.mjs';
import 'node:url';
import 'pathe';
import 'pkg-types';

function hookNuxtSeoProDataUpload() {
  const nuxt = useNuxt();
  const logger = useLogger("nuxt-seo-pro");
  const isBuild = !nuxt.options.dev && !nuxt.options._prepare;
  if (isBuild && !nuxt._isNuxtSeoProUploading) {
    const license = nuxt.options.runtimeConfig.seoProKey || process.env.NUXT_SEO_PRO_KEY;
    if (isTest || process.env.VITEST || !license) {
      return;
    }
    nuxt._isNuxtSeoProUploading = true;
    nuxt.hooks.hook("build:before", async () => {
      const siteConfig = useSiteConfig();
      const siteUrl = siteConfig.url?.startsWith("http") ? siteConfig.url : void 0;
      const siteName = siteConfig.name || void 0;
      const modules = detectNuxtSeoModules(nuxt);
      await nuxt.hooks.callHook("nuxt-seo-pro:modules", modules);
      await $fetch("https://nuxtseo.com/api/pro/verify", {
        method: "POST",
        body: {
          apiKey: license,
          siteUrl,
          siteName,
          modules: modules.length > 0 ? modules : void 0
        }
      }).catch((err) => {
        logger.debug("Pro data upload failed", err);
      });
    });
  }
}

export { hookNuxtSeoProDataUpload };
