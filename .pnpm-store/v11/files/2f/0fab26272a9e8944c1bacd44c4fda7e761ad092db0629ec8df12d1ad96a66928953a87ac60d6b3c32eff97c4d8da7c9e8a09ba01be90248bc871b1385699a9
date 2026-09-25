import { useNuxtApp, useRequestEvent } from "#app";
export function getSiteConfigStack() {
  return import.meta.server ? useRequestEvent()?.context.siteConfig : useNuxtApp().$nuxtSiteConfig;
}
