import { joinURL } from "ufo";
import { getHeader } from "#nuxtseo/h3";
import { defineCachedFunction } from "#nuxtseo/nitro";
import staticConfig from "#sitemap-virtual/static-config.mjs";
import { normaliseDate } from "../urlset/normalise.js";
import { parseChunkInfo } from "../utils/chunk.js";
import { getResolvedSitemapUrls } from "./sitemap.js";
const SERVER_CACHE_MAX_AGE = staticConfig.cacheMaxAgeSeconds || 60 * 10;
const buildSitemapIndexCached = defineCachedFunction(
  async (event, resolvers, runtimeConfig, nitro) => {
    return buildSitemapIndexInternal(resolvers, runtimeConfig, nitro);
  },
  {
    name: "sitemap:index",
    group: "sitemap",
    maxAge: SERVER_CACHE_MAX_AGE,
    base: "sitemap",
    // Use the sitemap storage
    getKey: (event) => {
      const host = getHeader(event, "host") || getHeader(event, "x-forwarded-host") || "";
      const proto = getHeader(event, "x-forwarded-proto") || "https";
      return `sitemap-index-${proto}-${host}`;
    },
    swr: true
    // Enable stale-while-revalidate
  }
);
async function buildSitemapIndexInternal(resolvers, runtimeConfig, nitro) {
  const {
    sitemaps,
    autoLastmod,
    defaultSitemapsChunkSize,
    sitemapsPathPrefix
  } = runtimeConfig;
  if (!sitemaps)
    throw new Error("Attempting to build a sitemap index without required `sitemaps` configuration.");
  const nonChunkedNames = [];
  const allFailedSources = [];
  for (const sitemapName in sitemaps) {
    if (sitemapName === "index" || sitemapName === "chunks")
      continue;
    const sitemapConfig = sitemaps[sitemapName];
    if (sitemapConfig.chunks || sitemapConfig._isChunking) {
      sitemapConfig._isChunking = true;
      sitemapConfig._chunkSize = sitemapConfig.chunkSize || (typeof sitemapConfig.chunks === "number" ? sitemapConfig.chunks : defaultSitemapsChunkSize || 1e3);
    } else {
      const chunkInfo = parseChunkInfo(sitemapName, sitemaps, defaultSitemapsChunkSize || void 0);
      if (!chunkInfo.isChunked)
        nonChunkedNames.push(sitemapName);
    }
  }
  const indexLastmod = autoLastmod ? normaliseDate(/* @__PURE__ */ new Date()) : void 0;
  const entries = [];
  const pushEntry = (name) => {
    const entry = {
      _sitemapName: name,
      sitemap: resolvers.canonicalUrlResolver(joinURL(sitemapsPathPrefix || "", `/${name}.xml`))
    };
    if (indexLastmod)
      entry.lastmod = indexLastmod;
    entries.push(entry);
  };
  if (typeof sitemaps.chunks !== "undefined") {
    const sitemap = sitemaps.chunks;
    const resolved = await getResolvedSitemapUrls(sitemap, "sitemap", true, resolvers, runtimeConfig, nitro);
    allFailedSources.push(...resolved.failedSources);
    const chunkCount = Math.ceil(resolved.urls.length / defaultSitemapsChunkSize);
    for (let i = 0; i < chunkCount; i++)
      pushEntry(String(i));
  }
  for (const name of nonChunkedNames)
    pushEntry(name);
  for (const sitemapName in sitemaps) {
    const sitemapConfig = sitemaps[sitemapName];
    if (sitemapName !== "index" && sitemapConfig._isChunking) {
      const chunkSize = sitemapConfig._chunkSize || defaultSitemapsChunkSize || 1e3;
      let chunkCount;
      if (typeof sitemapConfig.chunkCount === "number" && sitemapConfig.chunkCount > 0) {
        chunkCount = sitemapConfig.chunkCount;
      } else {
        const resolved = await getResolvedSitemapUrls(sitemapConfig, sitemapName, true, resolvers, runtimeConfig, nitro);
        allFailedSources.push(...resolved.failedSources);
        chunkCount = Math.ceil(resolved.urls.length / chunkSize);
      }
      sitemapConfig._chunkCount = chunkCount;
      for (let i = 0; i < chunkCount; i++)
        pushEntry(`${sitemapName}-${i}`);
    }
  }
  if (sitemaps.index) {
    entries.push(...sitemaps.index.sitemaps.map((entry) => {
      return typeof entry === "string" ? { sitemap: entry } : entry;
    }));
  }
  return { entries, failedSources: allFailedSources };
}
export async function buildSitemapIndex(resolvers, runtimeConfig, nitro) {
  if (!import.meta.dev && !import.meta.prerender && typeof runtimeConfig.cacheMaxAgeSeconds === "number" && runtimeConfig.cacheMaxAgeSeconds > 0 && resolvers.event) {
    return buildSitemapIndexCached(resolvers.event, resolvers, runtimeConfig, nitro);
  }
  return buildSitemapIndexInternal(resolvers, runtimeConfig, nitro);
}
export { urlsToIndexXml, urlsToIndexXmlStream } from "./index-xml.js";
