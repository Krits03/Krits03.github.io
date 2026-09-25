import { joinURL, withBase, withLeadingSlash, withoutLeadingSlash, withoutTrailingSlash } from "ufo";
import { appendHeader, createError, getRequestURL, getRouterParam, sendRedirect } from "#nuxtseo/h3";
import { useNitroApp, useRuntimeConfig } from "#nuxtseo/nitro";
import { useResolvedSitemapRuntimeConfig } from "../utils.js";
import { urlsToIndexXml, urlsToIndexXmlStream } from "./builder/index-xml.js";
import { buildSitemapIndex } from "./builder/sitemap-index.js";
import { createSitemap, renderSitemapOutput, setSitemapResponseHeaders, useNitroUrlResolvers } from "./nitro.js";
import { getSitemapConfig, parseChunkInfo } from "./utils/chunk.js";
export async function sitemapXmlEventHandler(e) {
  const runtimeConfig = await useResolvedSitemapRuntimeConfig(e);
  const { sitemaps } = runtimeConfig;
  if ("index" in sitemaps)
    return sendRedirect(e, withBase("/sitemap_index.xml", useRuntimeConfig().app.baseURL), import.meta.dev ? 302 : 301);
  return createSitemap(e, Object.values(sitemaps)[0], runtimeConfig);
}
export async function sitemapIndexXmlEventHandler(e) {
  const runtimeConfig = await useResolvedSitemapRuntimeConfig(e);
  const nitro = useNitroApp();
  const resolvers = useNitroUrlResolvers(e);
  const { entries: sitemaps, failedSources } = await buildSitemapIndex(resolvers, runtimeConfig, nitro);
  if (import.meta.prerender) {
    appendHeader(
      e,
      "x-nitro-prerender",
      sitemaps.filter((entry) => !!entry._sitemapName).map((entry) => encodeURIComponent(joinURL(runtimeConfig.sitemapsPathPrefix || "", `/${entry._sitemapName}.xml`))).join(", ")
    );
  }
  const indexResolvedCtx = { sitemaps, event: e };
  await nitro.hooks.callHook("sitemap:index-resolved", indexResolvedCtx);
  const errorInfo = failedSources.length > 0 ? { messages: failedSources.map((f) => f.error), urls: failedSources.map((f) => f.url) } : void 0;
  const output = await renderSitemapOutput(
    nitro,
    e,
    "sitemap",
    () => urlsToIndexXml(indexResolvedCtx.sitemaps, resolvers, runtimeConfig, errorInfo),
    () => urlsToIndexXmlStream(indexResolvedCtx.sitemaps, resolvers, runtimeConfig, errorInfo),
    !!runtimeConfig.experimentalStreaming && !import.meta.prerender,
    runtimeConfig.debug
  );
  setSitemapResponseHeaders(e, runtimeConfig);
  return output;
}
export async function sitemapChildXmlEventHandler(e) {
  const pathname = getRequestURL(e).pathname;
  if (!pathname.endsWith(".xml"))
    return;
  const runtimeConfig = await useResolvedSitemapRuntimeConfig(e);
  const { sitemaps } = runtimeConfig;
  let sitemapName = getRouterParam(e, "sitemap");
  if (!sitemapName) {
    const match = pathname.match(/(?:\/__sitemap__\/)?(.+)\.xml$/);
    if (match)
      sitemapName = match[1];
  }
  if (!sitemapName)
    throw createError({ statusCode: 400, message: "Invalid sitemap request" });
  sitemapName = sitemapName.replace(/\.xml$/, "");
  sitemapName = withLeadingSlash(sitemapName);
  if (sitemapName.startsWith("/__sitemap__/"))
    sitemapName = sitemapName.replace("/__sitemap__/", "/");
  if (runtimeConfig.sitemapsPathPrefix) {
    const prefix = withLeadingSlash(runtimeConfig.sitemapsPathPrefix);
    if (sitemapName.startsWith(prefix))
      sitemapName = sitemapName.replace(prefix, "/");
  }
  sitemapName = withoutLeadingSlash(withoutTrailingSlash(sitemapName));
  const chunkInfo = parseChunkInfo(sitemapName, sitemaps, runtimeConfig.defaultSitemapsChunkSize);
  const isAutoChunked = typeof sitemaps.chunks !== "undefined" && !Number.isNaN(Number(sitemapName));
  const sitemapExists = Object.hasOwn(sitemaps, sitemapName) || Object.hasOwn(sitemaps, chunkInfo.baseSitemapName) || isAutoChunked;
  if (!sitemapExists)
    throw createError({ statusCode: 404, message: `Sitemap "${sitemapName}" not found.` });
  if (chunkInfo.isChunked && chunkInfo.chunkIndex !== void 0) {
    const baseSitemap = sitemaps[chunkInfo.baseSitemapName];
    if (baseSitemap && !baseSitemap.chunks && !baseSitemap._isChunking)
      throw createError({ statusCode: 404, message: `Sitemap "${chunkInfo.baseSitemapName}" does not support chunking.` });
    if (baseSitemap?._chunkCount !== void 0 && chunkInfo.chunkIndex >= baseSitemap._chunkCount)
      throw createError({ statusCode: 404, message: `Chunk ${chunkInfo.chunkIndex} does not exist for sitemap "${chunkInfo.baseSitemapName}".` });
  }
  const sitemapConfig = getSitemapConfig(sitemapName, sitemaps, runtimeConfig.defaultSitemapsChunkSize || void 0);
  return createSitemap(e, sitemapConfig, runtimeConfig);
}
