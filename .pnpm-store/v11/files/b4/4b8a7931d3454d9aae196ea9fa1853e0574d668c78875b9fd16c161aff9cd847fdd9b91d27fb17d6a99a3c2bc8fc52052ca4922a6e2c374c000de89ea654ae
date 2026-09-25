import { getHeader } from "#nuxtseo/h3";
import { defineCachedFunction, useNitroApp, useRuntimeConfig } from "#nuxtseo/nitro";
import staticConfig from "#sitemap-virtual/static-config.mjs";
import { normalizeRuntimeFilters } from "../utils-pure.js";
export * from "../utils-pure.js";
const SERVER_CACHE_MAX_AGE = staticConfig.cacheMaxAgeSeconds || 60 * 10;
function dynamicRuntimeConfig(e) {
  return useRuntimeConfig(e).sitemap;
}
function copyStaticSitemaps() {
  return Object.fromEntries(
    Object.entries(staticConfig.sitemaps).map(([name, sitemap]) => [name, {
      ...sitemap,
      include: normalizeRuntimeFilters("include" in sitemap ? sitemap.include : void 0),
      exclude: normalizeRuntimeFilters("exclude" in sitemap ? sitemap.exclude : void 0)
    }])
  );
}
export function useSitemapRuntimeConfig(e) {
  return Object.freeze({
    ...staticConfig,
    sitemaps: copyStaticSitemaps(),
    ...dynamicRuntimeConfig(e)
  });
}
function serializeFilters(filters) {
  if (!filters?.length)
    return void 0;
  return filters.map((f) => {
    if (f instanceof RegExp)
      return { regex: `/${f.source}/${f.flags}` };
    return f;
  });
}
async function resolveSitemapSitemaps(e, nitro) {
  const ctx = { sitemaps: copyStaticSitemaps(), event: e };
  await nitro.hooks.callHook("sitemap:sitemaps-resolved", ctx);
  const sitemaps = { ...ctx.sitemaps };
  for (const name of Object.keys(sitemaps)) {
    const sitemap = { ...sitemaps[name] };
    if (typeof sitemap.urls === "function")
      sitemap.urls = await sitemap.urls();
    sitemap.include = serializeFilters(sitemap.include);
    sitemap.exclude = serializeFilters(sitemap.exclude);
    sitemaps[name] = sitemap;
  }
  return sitemaps;
}
const resolveSitemapSitemapsCached = defineCachedFunction(
  resolveSitemapSitemaps,
  {
    name: "sitemap:runtime-sitemaps",
    group: "sitemap",
    maxAge: SERVER_CACHE_MAX_AGE,
    base: "sitemap",
    // nitro calls getKey with the full fn args (event, nitro)
    getKey: (e) => {
      const host = e && (getHeader(e, "host") || getHeader(e, "x-forwarded-host")) || "";
      const proto = e && getHeader(e, "x-forwarded-proto") || "https";
      return `runtime-sitemaps-${proto}-${host}`;
    },
    swr: true
  }
);
export async function useResolvedSitemapRuntimeConfig(e) {
  const maxAge = dynamicRuntimeConfig(e)?.cacheMaxAgeSeconds ?? staticConfig.cacheMaxAgeSeconds;
  const shouldCache = !import.meta.dev && !import.meta.prerender && typeof maxAge === "number" && maxAge > 0;
  const sitemaps = shouldCache ? await resolveSitemapSitemapsCached(e, useNitroApp()) : await resolveSitemapSitemaps(e, useNitroApp());
  return Object.freeze({
    ...staticConfig,
    sitemaps,
    ...dynamicRuntimeConfig(e)
  });
}
