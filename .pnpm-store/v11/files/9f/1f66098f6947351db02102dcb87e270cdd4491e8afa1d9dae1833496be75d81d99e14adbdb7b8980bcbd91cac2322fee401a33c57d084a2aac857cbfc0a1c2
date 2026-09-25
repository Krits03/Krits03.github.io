import { SiteConfigPriority } from "site-config-stack";
import { defineNuxtPlugin, useRuntimeConfig } from "#app";
import { getSiteConfigStack } from "./i18n-shared.js";
export default defineNuxtPlugin({
  name: "nuxt-site-config:i18n",
  // @ts-expect-error untyped
  dependsOn: ["i18n-plugin-loader"],
  setup(nuxtApp) {
    const { $getLocale, $getLocales, $ts } = nuxtApp;
    const runtimeConfig = useRuntimeConfig();
    const locale = $getLocale();
    const locales = $getLocales();
    const defaultLocale = runtimeConfig.public.i18nConfig?.defaultLocale;
    const localeDefinition = locales.find((l) => l.code === locale) || locales.find((l) => l.code === defaultLocale);
    const stack = getSiteConfigStack();
    stack.push({
      _priority: import.meta.server ? SiteConfigPriority.i18n : SiteConfigPriority.build,
      _context: "nuxt-i18n-micro",
      currentLocale: localeDefinition.language || localeDefinition.iso || locale,
      // @ts-expect-error untyped
      description: $ts("nuxtSiteConfig.description", {}, ""),
      // @ts-expect-error untyped
      name: $ts("nuxtSiteConfig.name", {}, "")
    });
  }
});
