import { useNuxt, hasNuxtModule, addTypeTemplate, addTemplate, defineNuxtModule, createResolver, getNuxtModuleVersion, hasNuxtModuleCompatibility, addServerImports, addPrerenderRoutes, addServerPlugin, resolveModule, addServerHandler } from '@nuxt/kit';
import { defu } from 'defu';
import { withSiteUrl, installNuxtSiteConfig } from 'nuxt-site-config/kit';
import { isPathFile } from 'nuxt-site-config/urls';
import { isNuxtGenerate, renderNitroTypeAugmentations, useModuleLogger, setupNitroRuntimeCompatibility, getNuxtModuleOptions, resolveNitroPreset, resolveContentProvider, setupContentRuntime, createPagesPromise, createNitroPromise } from 'nuxtseo-shared/kit';
import { serializeFilters } from 'nuxtseo-shared/utils';
import { dirname, extname } from 'pathe';
import { readPackageJSON } from 'pkg-types';
import { withBase, withHttps, withTrailingSlash, withoutLeadingSlash, joinURL, withLeadingSlash } from 'ufo';
import { setupDevToolsUI as setupDevToolsUI$1 } from 'nuxtseo-shared/devtools';
import { once } from 'node:events';
import { readFileSync, statSync } from 'node:fs';
import { rm, mkdir, writeFile } from 'node:fs/promises';
import { join, resolve } from 'node:path';
import { pathToFileURL } from 'node:url';
import { Worker, MessageChannel } from 'node:worker_threads';
import { colors } from 'consola/utils';
import { splitForLocales, createPathFilter } from '../dist/runtime/utils-pure.js';
import { p as parseHtmlExtractSitemapMeta } from './shared/sitemap.BoMnWHOt.mjs';
import { normaliseDate } from '../dist/runtime/server/sitemap/urlset/normalise.js';
import { mapPathForI18nPages, splitPathForI18nLocales as splitPathForI18nLocales$1, expandCompactLocaleRoute, normalizeLocales, generatePathForI18nPages } from 'nuxtseo-shared/i18n';
import 'ultrahtml';

const COMARK_CONTENT_SOURCE = "@harlan-zw/comark-content:urls";
const COMARK_CONTENT_SITEMAP_ROUTE = "/__sitemap__/comark-content-urls.json";

function setupDevToolsUI(_options, resolve, nuxt = useNuxt()) {
  setupDevToolsUI$1(
    { route: "/__nuxt-sitemap", name: "sitemap", title: "Sitemap", icon: "carbon:load-balancer-application" },
    resolve,
    nuxt
  );
}

function formatPrerenderRoute(route) {
  let str = `  \u251C\u2500 ${route.route} (${route.generateTimeMS}ms)`;
  if (route.error) {
    const errorColor = colors[route.error.statusCode === 404 ? "yellow" : "red"];
    const errorLead = "\u2514\u2500\u2500";
    str += `
  \u2502 ${errorLead} ${errorColor(route.error.message)}`;
  }
  return colors.gray(str);
}
function includesSitemapRoot(sitemapName, routes) {
  return routes.includes(`/__sitemap__/`) || routes.includes(`/sitemap.xml`) || routes.includes(`/${sitemapName}`) || routes.includes("/sitemap_index.xml");
}
const NuxtRedirectHtmlRegex = /<!DOCTYPE html><html><head><meta http-equiv="refresh" content="0; url=([^"]+)"><\/head><\/html>/;
function setupPrerenderHandler(_options, nuxt = useNuxt()) {
  const { runtimeConfig: options, logger, generateGlobalSources, generateChildSources, prerenderSitemap } = _options;
  nuxt.options.nitro.prerender = nuxt.options.nitro.prerender || {};
  nuxt.options.nitro.prerender.routes = nuxt.options.nitro.prerender.routes || [];
  const shouldHookIntoPrerender = prerenderSitemap || nuxt.options.nitro.prerender.routes.length && nuxt.options.nitro.prerender.crawlLinks;
  if (isNuxtGenerate() && options.debug) {
    nuxt.options.nitro.prerender.routes.push("/__sitemap__/debug.json");
    logger.info("Adding debug route for sitemap generation:", colors.cyan("/__sitemap__/debug.json"));
  }
  if (!shouldHookIntoPrerender) {
    return;
  }
  nuxt.options.nitro.prerender.routes = nuxt.options.nitro.prerender.routes.filter((r) => r && !includesSitemapRoot(options.sitemapName, [r]));
  const runtimeAssetsPath = join(nuxt.options.rootDir, "node_modules/.cache/nuxt/sitemap");
  const localeCodes = options.autoI18n ? new Set(options.autoI18n.locales.map((l) => l.code)) : void 0;
  nuxt.hooks.hook("nitro:config", (nitroConfig) => {
    nitroConfig.virtual = nitroConfig.virtual || {};
    nitroConfig.virtual["#sitemap-virtual/read-sources.mjs"] = `
import { readFile } from 'node:fs/promises'
import { join } from 'pathe'

export async function readSourcesFromFilesystem(filename) {
  if (!import.meta.prerender) {
    return null
  }
  const path = join(${JSON.stringify(runtimeAssetsPath)}, filename)
  const data = await readFile(path, 'utf-8').catch(() => null)
  return data ? JSON.parse(data) : null
}
`;
  });
  nuxt.hooks.hook("nitro:init", async (nitro) => {
    let prerendererNitro = nitro;
    nitro.hooks.hook("prerender:init", (prerenderer) => {
      prerendererNitro = prerenderer;
    });
    await Promise.all([
      rm(join(runtimeAssetsPath, "global-sources.json"), { force: true }),
      rm(join(runtimeAssetsPath, "child-sources.json"), { force: true })
    ]);
    nitro.hooks.hook("prerender:generate", async (route) => {
      const html = route.contents;
      if (!route.fileName?.endsWith(".html") || !html || ["/200.html", "/404.html"].includes(route.route))
        return;
      if (NuxtRedirectHtmlRegex.test(html)) {
        route._sitemap = { loc: route.route, _sitemap: false };
        return;
      }
      const extractedMeta = parseHtmlExtractSitemapMeta(html, {
        images: options.discoverImages,
        videos: options.discoverVideos,
        // TODO configurable?
        lastmod: true,
        // when autoI18n is enabled, let the sitemap builder generate alternatives
        // based on i18n config instead of extracting from HTML (which can be incomplete)
        // when autoI18n is explicitly disabled, don't extract alternatives from HTML at all
        alternatives: !options.autoI18n && !options.hasDisabledAutoI18n,
        resolveUrl(s) {
          return s.startsWith("/") ? withSiteUrl(s) : s;
        }
      });
      if (extractedMeta === null) {
        route._sitemap = {
          loc: route.route,
          _sitemap: false
        };
        return;
      }
      route._sitemap = defu(route._sitemap, {
        loc: route.route
      });
      if (options.autoI18n && Object.keys(options.sitemaps).length > 1) {
        const path = route.route;
        const match = splitForLocales(path, localeCodes);
        const locale = match[0] || options.autoI18n.defaultLocale;
        if (options.isI18nMapped) {
          const { _sitemap } = options.autoI18n.locales.find((l) => l.code === locale) || { _sitemap: locale };
          route._sitemap._sitemap = _sitemap;
        }
      }
      route._sitemap = defu(extractedMeta, route._sitemap);
    });
    nitro.hooks.hook("prerender:done", async () => {
      const globalSources = await generateGlobalSources();
      const childSources = await generateChildSources();
      await mkdir(runtimeAssetsPath, { recursive: true });
      await writeFile(join(runtimeAssetsPath, "global-sources.json"), JSON.stringify(globalSources));
      await writeFile(join(runtimeAssetsPath, "child-sources.json"), JSON.stringify(childSources));
      const sitemapEntry = options.isMultiSitemap ? "/sitemap_index.xml" : `/${Object.keys(options.sitemaps)[0]}`;
      const prerenderServer = await loadPrerenderServer(prerendererNitro);
      await prerenderSitemapsFromEntry(nitro, prerenderServer.fetch, sitemapEntry).then((sitemaps) => nuxt.hooks.callHook("sitemap:prerender:done", { options, sitemaps })).finally(prerenderServer.close);
    });
  });
}
const PrerenderWorkerCode = `
const { parentPort, workerData } = require('node:worker_threads')

;(async () => {
  const serverEntry = await import(workerData.entry)
  const server = serverEntry.default
  const localFetch = serverEntry.localFetch
  const fetch = typeof server?.fetch === 'function'
    ? (input, headers) => server.fetch(new Request(new URL(input, 'http://localhost'), { headers }))
    : typeof localFetch === 'function'
      // older nitropack exposes an ofetch instance: a bare call returns parsed data, .raw returns the response
      ? (input, headers) => (localFetch.raw ?? localFetch)(input, { headers })
      : undefined
  const close = typeof server?.close === 'function'
    ? () => server.close()
    : typeof serverEntry.closePrerenderer === 'function'
      ? () => serverEntry.closePrerenderer()
      : async () => {}

  parentPort.postMessage(fetch ? { _tag: 'Ready' } : { _tag: 'Err', message: 'Nitro prerender server does not expose a fetch handler' })
  parentPort.on('message', ({ _tag, input, headers, port }) => {
    const task = _tag === 'Fetch'
      ? fetch(input, headers).then(async response => ({
          _tag: 'Ok',
          status: response.status,
          statusText: response.statusText,
          headers: [...response.headers],
          body: await response.arrayBuffer(),
        }))
      : close().then(() => ({ _tag: 'Ok' }))
    task.catch(error => ({ _tag: 'Err', message: error instanceof Error ? error.message : String(error) }))
      .then(result => port.postMessage(result, result.body ? [result.body] : []))
  })
})().catch(error => parentPort.postMessage({ _tag: 'Err', message: error instanceof Error ? error.message : String(error) }))
`;
function raceWithTimeout(promises, ms, message) {
  let timer;
  const timeout = new Promise((_, reject) => {
    timer = setTimeout(() => reject(new Error(message)), ms);
  });
  return Promise.race([...promises, timeout]).finally(() => clearTimeout(timer));
}
async function loadPrerenderServer(nitro) {
  const entryFileNames = nitro.options.rollupConfig?.output?.entryFileNames;
  const serverFilename = typeof entryFileNames === "string" ? entryFileNames : "index.mjs";
  const worker = new Worker(PrerenderWorkerCode, {
    eval: true,
    workerData: { entry: pathToFileURL(resolve(nitro.options.output.serverDir, serverFilename)).href }
  });
  const workerDead = new Promise((_, reject) => {
    worker.once("exit", (code) => reject(new Error(`The Nitro prerender server worker exited unexpectedly (code ${code})`)));
    worker.once("error", (error) => reject(error));
  });
  workerDead.catch(() => {
  });
  try {
    const [ready] = await raceWithTimeout([once(worker, "message"), workerDead], 6e4, "The Nitro prerender server did not become ready in time");
    if (ready._tag === "Err")
      throw new Error(ready.message);
  } catch (error) {
    await worker.terminate();
    throw error;
  }
  const callWorker = async (message) => {
    const { port1, port2 } = new MessageChannel();
    worker.postMessage({ ...message, port: port2 }, [port2]);
    try {
      const [result] = await Promise.race([once(port1, "message"), workerDead]);
      if (result._tag === "Err")
        throw new Error(result.message);
      return result;
    } finally {
      port1.close();
    }
  };
  return {
    async fetch(input, headers) {
      const { _tag, body, ...responseInit } = await callWorker({ _tag: "Fetch", input, headers });
      return new Response(body, responseInit);
    },
    async close() {
      try {
        await raceWithTimeout([callWorker({ _tag: "Close" })], 3e3, "The Nitro prerender server did not close in time");
      } catch {
      }
      await worker.terminate();
    }
  };
}
async function prerenderSitemapsFromEntry(nitro, fetch, entry) {
  const sitemaps = [];
  const queue = [entry];
  const processed = /* @__PURE__ */ new Set();
  while (queue.length) {
    const route = queue.shift();
    if (processed.has(route))
      continue;
    processed.add(route);
    const { filePath, prerenderUrls } = await prerenderRoute(nitro, fetch, route);
    sitemaps.push({
      name: route,
      get content() {
        return readFileSync(filePath, { encoding: "utf8" });
      }
    });
    queue.push(...prerenderUrls);
  }
  return sitemaps;
}
async function prerenderRoute(nitro, fetch, route) {
  const start = Date.now();
  const _route = { route, fileName: route };
  const encodedRoute = encodeURI(route);
  const fetchUrl = withBase(encodedRoute, nitro.options.baseURL);
  const res = await fetch(fetchUrl, { "x-nitro-prerender": encodedRoute });
  if (!res.ok)
    throw new Error(`Failed to prerender '${fetchUrl}': ${res.status} ${res.statusText}`);
  const header = res.headers.get("x-nitro-prerender") || "";
  const prerenderUrls = header.split(",").map((i) => decodeURIComponent(i.trim())).filter(Boolean);
  const filePath = join(nitro.options.output.publicDir, _route.fileName);
  await mkdir(dirname(filePath), { recursive: true });
  const content = await res.text();
  await writeFile(filePath, content, "utf8");
  _route.generateTimeMS = Date.now() - start;
  nitro._prerenderedRoutes.push(_route);
  nitro.logger.log(formatPrerenderRoute(_route));
  return { filePath, prerenderUrls };
}

function registerTypeTemplates(nitroCompatibility) {
  const hasRobotsModule = hasNuxtModule("@nuxtjs/robots") || hasNuxtModule("nuxt-simple-robots");
  addTypeTemplate({
    filename: "types/nuxt-sitemap-augments.d.ts",
    getContents: () => {
      const robotsType = hasRobotsModule ? "" : "robots?: boolean\n";
      const routeRules = `${robotsType}sitemap?: SitemapItemDefaults | false`;
      const runtimeHooks = `'sitemap:index-resolved': (ctx: SitemapIndexRenderCtx<${nitroCompatibility.eventType}>) => void | Promise<void>
'sitemap:input': (ctx: SitemapInputCtx<${nitroCompatibility.eventType}>) => void | Promise<void>
'sitemap:resolved': (ctx: SitemapRenderCtx<${nitroCompatibility.eventType}>) => void | Promise<void>
'sitemap:output': (ctx: SitemapOutputHookCtx<${nitroCompatibility.eventType}>) => void | Promise<void>
'sitemap:sources': (ctx: SitemapSourcesHookCtx<${nitroCompatibility.eventType}>) => void | Promise<void>
'sitemap:sitemaps-resolved': (ctx: SitemapsResolvedCtx<${nitroCompatibility.eventType}>) => void | Promise<void>`;
      const nitroTypes = renderNitroTypeAugmentations(nitroCompatibility, {
        nitroInterfaces: {
          PrerenderRoute: "_sitemap?: SitemapUrl"
        },
        routeConfig: routeRules,
        routeRules,
        runtimeHooks
      });
      return `// Generated by @nuxtjs/sitemap
/// <reference path="./nuxt-sitemap-virtual.d.ts" />
import type { SitemapUrl, SitemapItemDefaults, SitemapIndexRenderCtx, SitemapInputCtx, SitemapRenderCtx, SitemapOutputHookCtx, SitemapSourcesHookCtx, SitemapsResolvedCtx } from '@nuxtjs/sitemap'

${nitroTypes}

declare module 'vue-router' {
  interface RouteMeta {
    sitemap?: SitemapItemDefaults | false
  }
}

declare module '#app' {
  interface PageMeta {
    sitemap?: SitemapItemDefaults | false
  }
}

declare module 'nuxt/app' {
  interface PageMeta {
    sitemap?: SitemapItemDefaults | false
  }
}

export {}
`;
    }
  }, {
    nitro: true,
    node: true,
    nuxt: true
  });
  addTemplate({
    filename: "types/nuxt-sitemap-virtual.d.ts",
    getContents: () => `declare module '#sitemap-virtual/read-sources.mjs' {
  export function readSourcesFromFilesystem(filename: string): Promise<any | null>
}

declare module '#sitemap-virtual/global-sources.mjs' {
  import type { SitemapSourceBase, SitemapSourceResolved } from '#sitemap/types'

  export const sources: (SitemapSourceBase | SitemapSourceResolved)[]
}

declare module '#sitemap-virtual/child-sources.mjs' {
  import type { SitemapSourceBase, SitemapSourceResolved } from '#sitemap/types'

  export const sources: Record<string, (SitemapSourceBase | SitemapSourceResolved)[]>
}

declare module '#sitemap/content-filters' {
  export const filters: Map<string, (entry: any) => boolean>
}

declare module '#sitemap/content-on-url' {
  export const onUrlFns: Map<string, (url: Record<string, unknown>, entry: any, collection: string) => void>
}
`
  });
}

function splitPathForI18nLocales(path, autoI18n) {
  if (typeof path !== "string")
    return path;
  return splitPathForI18nLocales$1(path, autoI18n);
}
function uniquePaths(paths) {
  return [...new Set(paths)];
}
function resolveI18nFilterPaths(path, autoI18n) {
  if (typeof path !== "string")
    return [path];
  const mappedPaths = mapPathForI18nPages(path, autoI18n);
  if (mappedPaths === false) {
    if (autoI18n.strategy === "no_prefix")
      return [path];
    const splitPaths = splitPathForI18nLocales$1(path, autoI18n);
    return Array.isArray(splitPaths) ? splitPaths : [splitPaths];
  }
  if (autoI18n.strategy === "prefix" || autoI18n.strategy === "no_prefix")
    return uniquePaths(mappedPaths);
  const defaultLocales = autoI18n.locales.filter((locale) => locale.code === autoI18n.defaultLocale);
  const defaultStrategy = autoI18n.strategy === "prefix_and_default" ? "prefix" : "no_prefix";
  const defaultPaths = mapPathForI18nPages(path, {
    ...autoI18n,
    locales: defaultLocales,
    strategy: defaultStrategy
  });
  return uniquePaths([
    ...defaultPaths || [path],
    ...mappedPaths
  ]);
}

async function resolveUrls(urls, ctx) {
  try {
    if (typeof urls === "function")
      urls = urls();
    urls = await urls;
  } catch (e) {
    ctx.logger.error(`Failed to resolve ${typeof urls} urls.`);
    ctx.logger.error(e);
    return [];
  }
  try {
    urls = JSON.parse(JSON.stringify(urls));
  } catch (e) {
    ctx.logger.error(`Failed to serialize ${typeof urls} \`${ctx.path}\`, please make sure that the urls resolve as a valid array without circular dependencies.`);
    ctx.logger.error(e);
    return [];
  }
  return urls;
}
function deepForEachPage(pages, callback, opts, fullpath = null, depth = 0) {
  pages.forEach((page) => {
    let currentPath;
    if (page.path.startsWith("/")) {
      currentPath = page.path;
    } else {
      currentPath = page.path === "" ? fullpath : `${fullpath.replace(/\/$/, "")}/${page.path}`;
    }
    let didCallback = false;
    const compacted = expandCompactLocaleRoute(currentPath || "", opts.normalisedLocales.map((l) => l.code));
    if (compacted) {
      for (const { locale, path: localizedPath } of compacted) {
        const subPage = { ...page };
        subPage.name = `${page.name || ""}${opts.routesNameSeparator}${locale}`;
        subPage.path = localizedPath;
        callback(subPage, localizedPath, depth);
        didCallback = true;
      }
    }
    if (!didCallback) {
      callback(page, currentPath || "", depth);
    }
    if (page.children) {
      deepForEachPage(page.children, callback, opts, currentPath, depth + 1);
    }
  });
}
function convertNuxtPagesToSitemapEntries(pages, config) {
  const pathFilter = createPathFilter(config.filter);
  const routesNameSeparator = config.routesNameSeparator || "___";
  let flattenedPages = [];
  deepForEachPage(
    pages,
    (page, loc, depth) => {
      flattenedPages.push({ page, loc, depth });
    },
    {
      ...config,
      routesNameSeparator: config.routesNameSeparator || "___"
    }
  );
  flattenedPages = flattenedPages.filter((page) => !page.loc.includes(":")).filter((page, idx, arr) => {
    return !arr.some((p) => {
      return p.loc === page.loc && p.depth > page.depth;
    });
  }).map((p) => {
    delete p.depth;
    return p;
  });
  if (config.strategy === "prefix_and_default") {
    flattenedPages = flattenedPages.filter((p) => {
      if (p.page?.name) {
        const [, locale] = p.page.name.split(routesNameSeparator);
        return locale !== config.defaultLocale || p.page.name.endsWith("__default");
      }
      return true;
    });
  }
  const pagesWithMeta = flattenedPages.map((p) => {
    if (config.autoLastmod && p.page.file) {
      const stats = statSync(p.page.file, { throwIfNoEntry: false });
      if (stats?.mtime)
        p.lastmod = stats.mtime;
    }
    if (p.page?.meta?.sitemap) {
      p = defu(p.page.meta.sitemap, p);
    }
    return p;
  });
  const localeGroups = {};
  pagesWithMeta.reduce((acc, e) => {
    if (e.page.name?.includes(routesNameSeparator)) {
      const [name, locale] = e.page.name.split(routesNameSeparator);
      if (!name)
        return acc;
      if (!acc[name])
        acc[name] = [];
      const { _sitemap } = config.normalisedLocales.find((l) => l.code === locale) || { _sitemap: locale };
      acc[name].push({ ...e, _sitemap: config.isI18nMapped ? _sitemap : void 0, locale });
    } else {
      acc.default = acc.default || [];
      acc.default.push(e);
    }
    return acc;
  }, localeGroups);
  return Object.entries(localeGroups).map(([locale, entries]) => {
    if (locale === "default") {
      return entries.map((e) => {
        const [name] = (e.page?.name || "").split(routesNameSeparator);
        if (!name)
          return false;
        if (localeGroups[name]?.some((a) => a.locale === config.defaultLocale))
          return false;
        const defaultLocale = config.normalisedLocales.find((l) => l.code === config.defaultLocale);
        if (defaultLocale && config.isI18nMapped)
          e._sitemap = defaultLocale._sitemap;
        delete e.page;
        delete e.locale;
        return { ...e };
      }).filter(Boolean);
    }
    return entries.map((entry) => {
      const alternatives = config.autoI18n ? entries.map((entry2) => {
        const locale2 = config.normalisedLocales.find((l) => l.code === entry2.locale);
        if (!pathFilter(entry2.loc))
          return false;
        const href = locale2?.domain ? withHttps(withBase(entry2.loc, locale2?.domain)) : entry2.loc;
        return {
          hreflang: locale2?._hreflang,
          href
        };
      }).filter(Boolean) : [];
      if (config.autoI18n) {
        const xDefault = entries.find((a) => a.locale === config.defaultLocale);
        if (xDefault && alternatives.length && pathFilter(xDefault.loc)) {
          const locale2 = config.normalisedLocales.find((l) => l.code === xDefault.locale);
          const href = locale2?.domain ? withHttps(withBase(xDefault.loc, locale2?.domain)) : xDefault.loc;
          alternatives.push({
            hreflang: "x-default",
            href
          });
        }
      }
      const e = { ...entry };
      if (config.isI18nMapped) {
        const { _sitemap } = config.normalisedLocales.find((l) => l.code === entry.locale) || { _sitemap: locale };
        e._sitemap = _sitemap;
      }
      delete e.page;
      delete e.locale;
      return {
        ...e,
        ...alternatives.length ? { alternatives } : {}
      };
    });
  }).filter(Boolean).flat();
}
function generateExtraRoutesFromNuxtConfig(nuxt = useNuxt()) {
  const filterForValidPage = (p) => typeof p === "string" && !!p && !extname(p) && !p.startsWith("/api/") && !p.startsWith("/_");
  const routeRules = Object.entries(nuxt.options.routeRules || {}).filter(([k, v]) => {
    if (k.includes("*") || k.includes(".") || k.includes(":"))
      return false;
    if ("robots" in v && typeof v.robots === "boolean" && !v.robots)
      return false;
    return !v.redirect;
  }).map(([k]) => k).filter(filterForValidPage);
  return { routeRules };
}
function resolveExcludedAppSources(resolved, authored) {
  if (resolved === true || authored === true)
    return true;
  if (!Array.isArray(authored))
    return resolved;
  const excluded = [...resolved];
  for (const source of authored) {
    if (typeof source === "string" && !excluded.includes(source))
      excluded.push(source);
  }
  return excluded;
}

const IMAGE_TAGS = /* @__PURE__ */ new Set(["image", "img", "nuxtimg", "nuxt-img"]);
function discoverContentImages(body) {
  const images = [];
  const walk = (nodes) => {
    for (const node of nodes || []) {
      if (!Array.isArray(node) || typeof node[0] !== "string")
        continue;
      if (IMAGE_TAGS.has(node[0]) && node[1]?.src)
        images.push({ loc: node[1].src });
      walk(node.slice(2));
    }
  };
  walk(body?.value ?? body?.nodes);
  return images;
}
const module$1 = defineNuxtModule({
  meta: {
    name: "@nuxtjs/sitemap",
    compatibility: {
      nuxt: ">=3.9.0"
    },
    configKey: "sitemap"
  },
  moduleDependencies: {
    "@nuxtjs/i18n": {
      version: ">=8",
      optional: true
    },
    "nuxt-i18n-micro": {
      version: ">=1",
      optional: true
    },
    "nuxt-site-config": {
      version: ">=3.2"
    },
    "@nuxt/content": {
      version: ">=2",
      optional: true
    },
    "@harlan-zw/comark-content": {
      version: ">=0.1.2",
      optional: true
    },
    "@nuxtjs/robots": {
      version: ">=4",
      optional: true
    }
  },
  defaults: {
    enabled: true,
    credits: true,
    cacheMaxAgeSeconds: 60 * 10,
    // cache for 10 minutes
    minify: false,
    debug: false,
    experimentalStreaming: false,
    defaultSitemapsChunkSize: 1e3,
    autoLastmod: false,
    discoverImages: true,
    discoverVideos: true,
    urls: [],
    sortEntries: true,
    sitemapsPathPrefix: "/__sitemap__/",
    xsl: "/__sitemap__/style.xsl",
    xslTips: true,
    strictNuxtContentPaths: false,
    runtimeCacheStorage: true,
    sitemapName: "sitemap.xml",
    // cacheControlHeader: 'max-age=600, must-revalidate',
    defaults: {},
    // index sitemap options filtering
    include: [],
    exclude: ["/_**"],
    // sources
    sources: [],
    excludeAppSources: [],
    zeroRuntime: false
  },
  async setup(config, nuxt) {
    const { resolve } = createResolver(import.meta.url);
    const { name, version } = await readPackageJSON(resolve("../package.json"));
    const logger = useModuleLogger(name, config, nuxt);
    if (config.enabled === false) {
      logger.debug("The module is disabled, skipping setup.");
      return;
    }
    const nitroCompatibility = setupNitroRuntimeCompatibility(nuxt);
    config.exclude.push(`${withTrailingSlash(nuxt.options.app.buildAssetsDir)}**`);
    nuxt.options.alias["#sitemap"] = resolve("./runtime");
    nuxt.options.nitro.alias = nuxt.options.nitro.alias || {};
    nuxt.options.nitro.alias["#sitemap"] = resolve("./runtime");
    nuxt.options.experimental.extraPageMetaExtractionKeys = nuxt.options.experimental.extraPageMetaExtractionKeys || [];
    nuxt.options.experimental.extraPageMetaExtractionKeys.push("sitemap");
    config.xslColumns = config.xslColumns || [
      { label: "URL", width: "50%" },
      { label: "Images", width: "25%", select: "count(image:image)" },
      {
        label: "Last Updated",
        width: "25%",
        select: "concat(substring(sitemap:lastmod,0,11),concat(' ', substring(sitemap:lastmod,12,5)),concat(' ', substring(sitemap:lastmod,20,6)))"
      }
    ];
    if (config.autoLastmod) {
      config.defaults = config.defaults || {};
      config.defaults.lastmod = normaliseDate(/* @__PURE__ */ new Date());
    }
    const normalizedSitemaps = typeof config.sitemaps === "boolean" ? {} : config.sitemaps || {};
    if (!nuxt.options._prepare && Object.keys(normalizedSitemaps).length) {
      const isSitemapIndexOnly = typeof normalizedSitemaps?.index !== "undefined" && Object.keys(normalizedSitemaps).length === 1;
      if (!isSitemapIndexOnly) {
        const warnForIgnoredKey = (key) => {
          logger.warn(`You are using multiple-sitemaps but have provided \`sitemap.${key}\` in your Nuxt config. This will be ignored, please move it to the child sitemap config.`);
          logger.warn("Learn more at: https://nuxtseo.com/sitemap/guides/multi-sitemaps");
        };
        switch (true) {
          case (config?.sources?.length || 0) > 0:
            warnForIgnoredKey("sources");
            break;
          case config?.includeAppSources !== void 0:
            warnForIgnoredKey("includeAppSources");
            break;
        }
      }
    }
    await installNuxtSiteConfig();
    const userGlobalSources = [
      ...config.sources || []
    ];
    const appGlobalSources = [];
    nuxt.options.nitro.storage = nuxt.options.nitro.storage || {};
    if (config.runtimeCacheStorage && !nuxt.options.dev && typeof config.runtimeCacheStorage === "object")
      nuxt.options.nitro.storage.sitemap = config.runtimeCacheStorage;
    if (!config.sitemapName.endsWith("xml")) {
      const newName = `${config.sitemapName.split(".")[0]}.xml`;
      logger.warn(`You have provided a \`sitemapName\` that does not end with \`.xml\`. This is not supported by search engines, renaming to \`${newName}\`.`);
      config.sitemapName = newName;
    }
    config.sitemapName = withoutLeadingSlash(config.sitemapName);
    let usingMultiSitemaps = !!config.sitemaps;
    let isI18nMapped = false;
    let nuxtI18nConfig = {};
    let resolvedAutoI18n = typeof config.autoI18n === "boolean" ? false : config.autoI18n || false;
    const hasDisabledAutoI18n = typeof config.autoI18n === "boolean" && !config.autoI18n;
    let normalisedLocales = [];
    let usingI18nPages = false;
    const i18nModule = ["@nuxtjs/i18n", "nuxt-i18n-micro"].find((s) => hasNuxtModule(s));
    if (i18nModule) {
      const i18nVersion = await getNuxtModuleVersion(i18nModule);
      if (i18nVersion && i18nModule === "@nuxtjs/i18n" && !await hasNuxtModuleCompatibility(i18nModule, ">=8"))
        logger.warn(`You are using ${i18nModule} v${i18nVersion}. For the best compatibility, please upgrade to ${i18nModule} v8.0.0 or higher.`);
      nuxtI18nConfig = await getNuxtModuleOptions(i18nModule) || {};
      normalisedLocales = normalizeLocales(nuxtI18nConfig);
      usingI18nPages = !!Object.keys(nuxtI18nConfig.pages || {}).length;
      if (usingI18nPages && !hasDisabledAutoI18n) {
        const i18nPagesSources = {
          context: {
            name: `${i18nModule}:pages`,
            description: "Generated from your i18n.pages config.",
            tips: [
              "You can disable this with `autoI18n: false`."
            ]
          },
          urls: []
        };
        for (const pageLocales of Object.values(nuxtI18nConfig?.pages)) {
          for (const localeCode in pageLocales) {
            const locale = normalisedLocales.find((l) => l.code === localeCode);
            if (!locale || !pageLocales[localeCode] || pageLocales[localeCode].includes("["))
              continue;
            const alternatives = Object.keys(pageLocales).filter((l) => pageLocales[l] !== false).map((l) => ({
              hreflang: normalisedLocales.find((nl) => nl.code === l)?._hreflang || l,
              // @ts-expect-error untyped
              href: generatePathForI18nPages({ localeCode: l, pageLocales: pageLocales[l], nuxtI18nConfig, normalisedLocales })
            }));
            if (alternatives.length && nuxtI18nConfig.defaultLocale && pageLocales[nuxtI18nConfig.defaultLocale] && pageLocales[nuxtI18nConfig.defaultLocale] !== false)
              alternatives.push({ hreflang: "x-default", href: generatePathForI18nPages({ normalisedLocales, localeCode: nuxtI18nConfig.defaultLocale, pageLocales: pageLocales[nuxtI18nConfig.defaultLocale], nuxtI18nConfig }) });
            i18nPagesSources.urls.push({
              _sitemap: locale._sitemap,
              loc: generatePathForI18nPages({ normalisedLocales, localeCode, pageLocales: pageLocales[localeCode], nuxtI18nConfig }),
              alternatives
            });
            if (nuxtI18nConfig.strategy === "prefix_and_default" && localeCode === nuxtI18nConfig.defaultLocale) {
              i18nPagesSources.urls.push({
                _sitemap: locale._sitemap,
                loc: generatePathForI18nPages({ normalisedLocales, localeCode, pageLocales: pageLocales[localeCode], nuxtI18nConfig, forcedStrategy: "prefix" }),
                alternatives
              });
            }
          }
        }
        appGlobalSources.push(i18nPagesSources);
        if (Array.isArray(config.excludeAppSources))
          config.excludeAppSources.push("nuxt:pages");
      } else {
        if (!normalisedLocales.length)
          logger.warn(`You are using ${i18nModule} but have not configured any locales, this will cause issues with ${name}. Please configure \`locales\`.`);
      }
      const hasSetAutoI18n = typeof config.autoI18n === "object" && Object.keys(config.autoI18n).length;
      const hasI18nConfigForAlternatives = nuxtI18nConfig.differentDomains || usingI18nPages || nuxtI18nConfig.strategy !== "no_prefix" && nuxtI18nConfig.locales;
      if (!hasSetAutoI18n && !hasDisabledAutoI18n && hasI18nConfigForAlternatives) {
        resolvedAutoI18n = {
          differentDomains: nuxtI18nConfig.differentDomains,
          defaultLocale: nuxtI18nConfig.defaultLocale,
          locales: normalisedLocales,
          strategy: nuxtI18nConfig.strategy,
          // @ts-expect-error untyped
          pages: nuxtI18nConfig.pages
        };
      }
      let canI18nMap = !hasDisabledAutoI18n && config.sitemaps !== false && nuxtI18nConfig.strategy !== "no_prefix";
      if (typeof config.sitemaps === "object") {
        const sitemapEntries = Object.entries(config.sitemaps).filter(([k]) => k !== "index");
        const isSitemapIndexOnly = sitemapEntries.length === 0;
        const hasIncludeAppSources = sitemapEntries.some(([_, v]) => v && typeof v === "object" && v.includeAppSources);
        if (!isSitemapIndexOnly && !hasIncludeAppSources)
          canI18nMap = false;
      }
      if (canI18nMap && resolvedAutoI18n) {
        const existingSitemaps = typeof config.sitemaps === "object" ? config.sitemaps : {};
        const i18nSitemaps = [];
        const nonI18nSitemaps = {};
        for (const [name2, cfg] of Object.entries(existingSitemaps)) {
          if (name2 === "index")
            continue;
          if (cfg && typeof cfg === "object" && cfg.includeAppSources) {
            i18nSitemaps.push({ name: name2, cfg });
          } else {
            nonI18nSitemaps[name2] = cfg;
          }
        }
        const newSitemaps = {
          index: [...existingSitemaps.index || [], ...config.appendSitemaps || []]
        };
        const hasCustomI18nSitemaps = i18nSitemaps.length > 0;
        if (hasCustomI18nSitemaps) {
          for (const { name: name2, cfg } of i18nSitemaps) {
            const { sitemapName: _sitemapName, _route, _isChunking, _chunkSize, _chunkCount, ...inheritedConfig } = cfg;
            for (const locale of resolvedAutoI18n.locales) {
              newSitemaps[`${locale._sitemap}-${name2}`] = {
                ...inheritedConfig,
                includeAppSources: true
              };
            }
          }
        } else {
          for (const locale of resolvedAutoI18n.locales) {
            newSitemaps[locale._sitemap] = { includeAppSources: true };
          }
        }
        Object.assign(newSitemaps, nonI18nSitemaps);
        config.sitemaps = newSitemaps;
        isI18nMapped = true;
        usingMultiSitemaps = true;
      }
    }
    nuxt.hooks.hook("robots:config", (robotsConfig) => {
      robotsConfig.sitemap.push(usingMultiSitemaps ? "/sitemap_index.xml" : `/${config.sitemapName}`);
    });
    nuxt.hooks.hook("modules:done", async () => {
      const robotsModuleName = ["nuxt-simple-robots", "@nuxtjs/robots"].find((s) => hasNuxtModule(s));
      let needsRobotsPolyfill = true;
      if (robotsModuleName) {
        const robotsVersion = await getNuxtModuleVersion(robotsModuleName);
        if (robotsVersion && !await hasNuxtModuleCompatibility(robotsModuleName, ">=4"))
          logger.warn(`You are using ${robotsModuleName} v${robotsVersion}. For the best compatibility, please upgrade to ${robotsModuleName} v4.0.0 or higher.`);
        else
          needsRobotsPolyfill = false;
      }
      if (needsRobotsPolyfill) {
        nuxt.options.nitro.alias = nuxt.options.nitro.alias || {};
        nuxt.options.nitro.alias["#internal/nuxt-robots"] = resolve("./runtime/server/robots-polyfill");
        addServerImports([{
          name: "getPathRobotConfig",
          as: "getPathRobotConfig",
          from: resolve("./runtime/server/robots-polyfill/getPathRobotConfig")
        }]);
      }
    });
    registerTypeTemplates(nitroCompatibility);
    const prerenderedRoutes = nuxt.options.nitro.prerender?.routes || [];
    let prerenderSitemap = isNuxtGenerate() || includesSitemapRoot(config.sitemapName, prerenderedRoutes);
    if (resolveNitroPreset() === "vercel-edge") {
      logger.warn("Runtime sitemaps are not supported on Vercel Edge, falling back to prerendering sitemaps.");
      prerenderSitemap = true;
    }
    if (config.zeroRuntime && !prerenderSitemap) {
      prerenderSitemap = true;
      addPrerenderRoutes("/sitemap.xml");
      if (!nuxt.options.dev)
        logger.info("`zeroRuntime` enabled - sitemap routes will be prerendered.");
    }
    const routesPath = config.zeroRuntime ? "./runtime/server/routes/__zero-runtime" : "./runtime/server/routes";
    const routeRules = {};
    nuxt.options.nitro.routeRules = nuxt.options.nitro.routeRules || {};
    if (prerenderSitemap) {
      routeRules.headers = {
        "Content-Type": "text/xml; charset=UTF-8",
        "Cache-Control": config.cacheMaxAgeSeconds ? `public, max-age=${config.cacheMaxAgeSeconds}, must-revalidate` : "no-cache, no-store",
        "X-Sitemap-Prerendered": (/* @__PURE__ */ new Date()).toISOString()
      };
    }
    const hasRouteRuleContent = Object.keys(routeRules).length > 0;
    if (usingMultiSitemaps) {
      nuxt.options.nitro.routeRules["/sitemap.xml"] = { redirect: withBase("/sitemap_index.xml", nuxt.options.app.baseURL) };
      if (hasRouteRuleContent) {
        nuxt.options.nitro.routeRules["/sitemap_index.xml"] = routeRules;
        if (typeof config.sitemaps === "object") {
          for (const k in config.sitemaps) {
            if (k === "index")
              continue;
            nuxt.options.nitro.routeRules[joinURL(config.sitemapsPathPrefix || "", `/${k}.xml`)] = routeRules;
            const sitemapConfig = config.sitemaps[k];
            if (sitemapConfig.chunks)
              nuxt.options.nitro.routeRules[joinURL(config.sitemapsPathPrefix || "", `/${k}-*.xml`)] = routeRules;
          }
        } else {
          nuxt.options.nitro.routeRules[joinURL(config.sitemapsPathPrefix || "", `/[0-9]+.xml`)] = routeRules;
        }
      }
    } else if (hasRouteRuleContent) {
      nuxt.options.nitro.routeRules[`/${config.sitemapName}`] = routeRules;
    }
    if (config.zeroRuntime && (config.experimentalWarmUp || config.experimentalCompression || config.experimentalStreaming))
      logger.warn("`experimentalWarmUp`, `experimentalCompression`, and `experimentalStreaming` are ignored in zeroRuntime mode.");
    if (!config.zeroRuntime) {
      if (config.experimentalWarmUp)
        addServerPlugin(resolve("./runtime/server/plugins/warm-up"));
      if (config.experimentalCompression)
        addServerPlugin(resolve("./runtime/server/plugins/compression"));
      if (config.experimentalStreaming || config.experimentalCompression)
        addServerPlugin(resolve("./runtime/server/plugins/stream-transport"));
    }
    const isNuxtContentDocumentDriven = !!nuxt.options.content?.documentDriven || config.strictNuxtContentPaths;
    const contentProvider = await resolveContentProvider(nuxt);
    const isNuxtContentV3 = contentProvider._tag === "NuxtContent" && contentProvider.version === 3;
    const isNuxtContentV2 = contentProvider._tag === "NuxtContent" && contentProvider.version === 2;
    const isComarkContent = contentProvider._tag === "Comark";
    const nuxtV3Collections = /* @__PURE__ */ new Set();
    setupContentRuntime(contentProvider, nuxt);
    const registerContentSitemapHook = (options) => {
      nuxt.hooks.hook("content:file:afterParse", (ctx) => {
        try {
          const content = ctx.content;
          nuxtV3Collections.add(ctx.collection.name);
          if (String(ctx.content.path).includes("/.")) {
            ctx.content.sitemap = null;
            return;
          }
          if (options.requireCollectionField && (!ctx.collection.fields || !("sitemap" in ctx.collection.fields))) {
            ctx.content.sitemap = null;
            return;
          }
          if (typeof content.sitemap !== "undefined" && !content.sitemap) {
            ctx.content.sitemap = null;
            return;
          }
          if (ctx.content.robots === false) {
            ctx.content.sitemap = null;
            return;
          }
          const images = [];
          if (config.discoverImages)
            images.push(...discoverContentImages(content.body));
          const lastmod = content.seo?.articleModifiedTime || content.updatedAt;
          const defaults = {
            loc: content.path
          };
          if (images.length > 0)
            defaults.images = images;
          if (lastmod)
            defaults.lastmod = lastmod;
          ctx.content.sitemap = defu(typeof content.sitemap === "object" ? content.sitemap : {}, defaults);
        } catch (e) {
          logger.warn(`Failed to process sitemap data for content file (collection: ${ctx.collection?.name}, path: ${ctx.content?.path}), skipping.`, e);
        }
      });
    };
    const addContentCallbackVirtuals = () => {
      nuxt.hook("nitro:config", (nitroConfig) => {
        const filterEntries = [];
        if (globalThis.__sitemapCollectionFilters) {
          for (const [name2, filterFn] of globalThis.__sitemapCollectionFilters.entries())
            filterEntries.push(`filters.set(${JSON.stringify(name2)}, ${filterFn.toString()})`);
        }
        const onUrlEntries = [];
        if (globalThis.__sitemapCollectionOnUrlFns) {
          for (const [name2, fn] of globalThis.__sitemapCollectionOnUrlFns.entries())
            onUrlEntries.push(`onUrlFns.set(${JSON.stringify(name2)}, ${fn.toString()})`);
        }
        nitroConfig.virtual = nitroConfig.virtual || {};
        nitroConfig.virtual["#sitemap/content-filters"] = `export const filters = new Map()
${filterEntries.join("\n")}`;
        nitroConfig.virtual["#sitemap/content-on-url"] = `export const onUrlFns = new Map()
${onUrlEntries.join("\n")}`;
      });
    };
    if (isNuxtContentV3) {
      if (nuxt.options._installedModules.some((m) => m.meta.name === "Content")) {
        logger.warn("You have loaded `@nuxt/content` before `@nuxtjs/sitemap`, this may cause issues with the integration. Please ensure `@nuxtjs/sitemap` is loaded first.");
      }
      config.exclude.push("/__nuxt_content/**");
      const needsCustomAlias = await hasNuxtModuleCompatibility("@nuxt/content", "<3.6.0");
      if (needsCustomAlias) {
        nuxt.options.alias["#sitemap/content-v3-nitro-path"] = resolve(dirname(resolveModule("@nuxt/content")), "runtime/nitro");
        nuxt.options.alias["@nuxt/content/nitro"] = resolve("./runtime/server/content-compat");
      }
      registerContentSitemapHook({ requireCollectionField: true });
      addContentCallbackVirtuals();
      addServerHandler({
        route: "/__sitemap__/nuxt-content-urls.json",
        handler: resolve("./runtime/server/routes/__sitemap__/content-urls")
      });
      if (config.strictNuxtContentPaths) {
        logger.warn("You have set `strictNuxtContentPaths: true` but are using @nuxt/content v3. This is not required, please remove it.");
      }
      appGlobalSources.push({
        context: {
          name: "@nuxt/content@v3:urls",
          description: "Generated from your markdown files.",
          tips: nuxtV3Collections.size ? [`Parsing the following collections: ${Array.from(nuxtV3Collections).join(", ")}`] : ["No collections found. Make sure your content collections have a `path` field."]
        },
        fetch: "/__sitemap__/nuxt-content-urls.json"
      });
    } else if (isComarkContent) {
      registerContentSitemapHook({ requireCollectionField: false });
      addContentCallbackVirtuals();
      addServerHandler({
        route: COMARK_CONTENT_SITEMAP_ROUTE,
        handler: resolve("./runtime/server/routes/__sitemap__/content-urls")
      });
      if (config.strictNuxtContentPaths) {
        logger.warn("You have set `strictNuxtContentPaths: true` but are using comark-content. This is not required, please remove it.");
      }
      appGlobalSources.push({
        context: {
          name: COMARK_CONTENT_SOURCE,
          description: "Generated from your markdown files.",
          tips: nuxtV3Collections.size ? [`Parsing the following collections: ${Array.from(nuxtV3Collections).join(", ")}`] : ["No collections found. Set `sitemap: false` on a collection to keep it out."]
        },
        fetch: COMARK_CONTENT_SITEMAP_ROUTE
      });
    } else if (isNuxtContentV2) {
      addServerPlugin(resolve("./runtime/server/plugins/nuxt-content-v2"));
      addServerHandler({
        route: "/__sitemap__/nuxt-content-urls.json",
        handler: resolve("./runtime/server/routes/__sitemap__/nuxt-content-urls-v2")
      });
      const tips = [];
      if (nuxt.options.content?.documentDriven)
        tips.push("Enabled because you're using `@nuxt/content` with `documentDriven: true`.");
      else if (config.strictNuxtContentPaths)
        tips.push("Enabled because you've set `config.strictNuxtContentPaths: true`.");
      else
        tips.push("You can provide a `sitemap` key in your markdown frontmatter to configure specific URLs. Make sure you include a `loc`.");
      appGlobalSources.push({
        context: {
          name: "@nuxt/content@v2:urls",
          description: "Generated from your markdown files.",
          tips
        },
        fetch: "/__sitemap__/nuxt-content-urls.json"
      });
    }
    const sitemaps = {};
    if (usingMultiSitemaps) {
      addServerHandler({
        route: "/sitemap_index.xml",
        handler: resolve(`${routesPath}/sitemap_index.xml`),
        lazy: true,
        middleware: false
      });
      if (config.sitemapsPathPrefix && config.sitemapsPathPrefix !== "/") {
        addServerHandler({
          route: joinURL(config.sitemapsPathPrefix, `/**:sitemap`),
          handler: resolve(`${routesPath}/sitemap/[sitemap].xml`),
          lazy: true,
          middleware: false
        });
      } else {
        const sitemapNames = Object.keys(config.sitemaps || {});
        let hasChunkedSitemaps = false;
        for (const sitemapName of sitemapNames) {
          if (sitemapName === "index")
            continue;
          const sitemapConfig = config.sitemaps[sitemapName];
          addServerHandler({
            route: withLeadingSlash(`${sitemapName}.xml`),
            handler: resolve(`${routesPath}/sitemap/[sitemap].xml`),
            lazy: true,
            middleware: false
          });
          if (sitemapConfig.chunks)
            hasChunkedSitemaps = true;
        }
        if (hasChunkedSitemaps) {
          const maxChunks = 20;
          for (const sitemapName of sitemapNames) {
            if (sitemapName === "index")
              continue;
            const sitemapConfig = config.sitemaps[sitemapName];
            if (sitemapConfig.chunks) {
              for (let i = 0; i < maxChunks; i++) {
                addServerHandler({
                  route: `/${sitemapName}-${i}.xml`,
                  handler: resolve(`${routesPath}/sitemap/[sitemap].xml`),
                  lazy: true,
                  middleware: false
                });
              }
            }
          }
        }
      }
      sitemaps.index = {
        sitemapName: "index",
        _route: withBase("sitemap_index.xml", nuxt.options.app.baseURL || "/"),
        // @ts-expect-error untyped
        sitemaps: [...config.sitemaps.index || [], ...config.appendSitemaps || []]
      };
      if (typeof config.sitemaps === "object") {
        for (const sitemapName in config.sitemaps) {
          if (sitemapName === "index")
            continue;
          const definition = config.sitemaps[sitemapName];
          const sitemapConfig = defu(
            {
              sitemapName,
              _route: withBase(joinURL(config.sitemapsPathPrefix || "", `${sitemapName}.xml`), nuxt.options.app.baseURL || "/"),
              _hasSourceChunk: typeof definition.urls !== "undefined" || definition.sources?.length
            },
            { ...definition, urls: void 0, sources: void 0 },
            { include: config.include, exclude: config.exclude }
          );
          if (definition.chunks) {
            let chunkSize = config.defaultSitemapsChunkSize || 1e3;
            if (typeof definition.chunks === "number") {
              if (definition.chunks <= 0) {
                logger.warn(`Invalid chunks value (${definition.chunks}) for sitemap "${sitemapName}". Using default.`);
              } else {
                chunkSize = definition.chunks;
              }
            }
            if (definition.chunkSize !== void 0) {
              if (typeof definition.chunkSize !== "number" || definition.chunkSize <= 0) {
                logger.warn(`Invalid chunkSize value (${definition.chunkSize}) for sitemap "${sitemapName}". Using default.`);
              } else {
                chunkSize = definition.chunkSize;
              }
            }
            sitemapConfig._isChunking = true;
            sitemapConfig._chunkSize = chunkSize;
            sitemapConfig.chunks = definition.chunks;
            sitemapConfig.chunkSize = definition.chunkSize;
          }
          sitemaps[sitemapName] = sitemapConfig;
        }
      } else {
        sitemaps.chunks = {
          sitemapName: "chunks",
          defaults: config.defaults,
          include: config.include,
          exclude: config.exclude,
          includeAppSources: true
        };
      }
    } else {
      sitemaps[config.sitemapName] = {
        sitemapName: config.sitemapName,
        route: withBase(config.sitemapName, nuxt.options.app.baseURL || "/"),
        // will contain the xml
        defaults: config.defaults,
        include: config.include,
        exclude: config.exclude,
        includeAppSources: true
      };
    }
    if (resolvedAutoI18n && usingI18nPages && !hasDisabledAutoI18n) {
      const i18n = resolvedAutoI18n;
      for (const sitemapName in sitemaps) {
        if (["index", "chunks"].includes(sitemapName))
          continue;
        const sitemap = sitemaps[sitemapName];
        sitemap.include = (sitemap.include || []).flatMap((path) => resolveI18nFilterPaths(path, i18n));
        sitemap.exclude = (sitemap.exclude || []).flatMap((path) => resolveI18nFilterPaths(path, i18n));
      }
    } else if (resolvedAutoI18n && resolvedAutoI18n.locales && resolvedAutoI18n.strategy !== "no_prefix") {
      const i18n = resolvedAutoI18n;
      for (const sitemapName in sitemaps) {
        if (["index", "chunks"].includes(sitemapName))
          continue;
        const sitemap = sitemaps[sitemapName];
        sitemap.include = (sitemap.include || []).map((path) => splitPathForI18nLocales(path, i18n)).flat();
        sitemap.exclude = (sitemap.exclude || []).map((path) => splitPathForI18nLocales(path, i18n)).flat();
      }
    }
    for (const sitemapName in sitemaps) {
      const sitemap = sitemaps[sitemapName];
      sitemap.include = serializeFilters(sitemap.include || [], "@nuxtjs/sitemap");
      sitemap.exclude = serializeFilters(sitemap.exclude || [], "@nuxtjs/sitemap");
    }
    const runtimeConfig = {
      isI18nMapped,
      sitemapName: config.sitemapName,
      isMultiSitemap: usingMultiSitemaps,
      excludeAppSources: config.excludeAppSources,
      cacheMaxAgeSeconds: nuxt.options.dev ? 0 : config.cacheMaxAgeSeconds,
      experimentalStreaming: config.experimentalStreaming,
      autoLastmod: config.autoLastmod,
      defaultSitemapsChunkSize: config.defaultSitemapsChunkSize,
      minify: config.minify,
      sortEntries: config.sortEntries,
      debug: config.debug,
      // needed for nuxt/content integration and prerendering
      discoverImages: config.discoverImages,
      discoverVideos: config.discoverVideos,
      sitemapsPathPrefix: config.sitemapsPathPrefix,
      /* @nuxt/content */
      isNuxtContentDocumentDriven,
      /* xsl styling */
      xsl: config.xsl,
      xslTips: config.xslTips,
      xslColumns: config.xslColumns,
      credits: config.credits,
      version,
      sitemaps
    };
    if (resolvedAutoI18n)
      runtimeConfig.autoI18n = resolvedAutoI18n;
    if (hasDisabledAutoI18n)
      runtimeConfig.hasDisabledAutoI18n = true;
    const dynamicRuntimeConfig = {
      cacheMaxAgeSeconds: runtimeConfig.cacheMaxAgeSeconds,
      debug: runtimeConfig.debug
    };
    const { debug: _d, ...staticRuntimeConfig } = runtimeConfig;
    nuxt.options.runtimeConfig.sitemap = dynamicRuntimeConfig;
    nuxt.hook("nitro:config", (nitroConfig) => {
      nitroConfig.virtual = nitroConfig.virtual || {};
      nitroConfig.virtual["#sitemap-virtual/static-config.mjs"] = `export default ${JSON.stringify(staticRuntimeConfig)}`;
    });
    if ((config.debug || nuxt.options.dev) && !(config.zeroRuntime && !nuxt.options.dev)) {
      addServerHandler({
        route: "/__sitemap__/debug.json",
        handler: resolve("./runtime/server/routes/__sitemap__/debug")
      });
      if (nuxt.options.dev) {
        addServerHandler({
          route: "/__sitemap__/debug-production.json",
          handler: resolve("./runtime/server/routes/__sitemap__/debug-production")
        });
      }
      if (usingMultiSitemaps) {
        addServerHandler({
          route: "/__sitemap__/**:sitemap",
          handler: resolve("./runtime/server/routes/sitemap/[sitemap].xml"),
          lazy: true,
          middleware: true
        });
      }
      setupDevToolsUI(config, resolve);
    }
    const imports = [
      {
        from: resolve("./runtime/server/composables/defineSitemapEventHandler"),
        name: "defineSitemapEventHandler"
      },
      {
        from: resolve("./runtime/server/composables/asSitemapUrl"),
        name: "asSitemapUrl"
      }
    ];
    addServerImports(imports);
    const pagesPromise = createPagesPromise();
    const nitroPromise = createNitroPromise();
    let resolvedConfigUrls = false;
    const isValidPrerenderRoute = (r) => {
      if (["/200.html", "/404.html", "/index.html"].includes(r.route) || r.error || isPathFile(r.route))
        return false;
      return r.contentType?.includes("text/html");
    };
    const generateGlobalSources = async () => {
      const excludedAppSources = resolveExcludedAppSources(
        config.excludeAppSources,
        nuxt.options.sitemap?.excludeAppSources
      );
      const { routeRules: routeRules2 } = generateExtraRoutesFromNuxtConfig();
      const nitro = await nitroPromise;
      const prerenderedRoutes2 = nitro._prerenderedRoutes || [];
      const prerenderUrlsFinal = [
        ...prerenderedRoutes2.filter(isValidPrerenderRoute).map((r) => {
          if (r._sitemap)
            return r._sitemap;
          if (r.route.startsWith("/api/") || r.route.startsWith("/_"))
            return void 0;
          return { loc: r.route };
        }).filter((entry) => entry && (typeof entry === "string" || entry._sitemap !== false))
      ];
      if (config.debug) {
        logger.info("Prerendered routes:", prerenderUrlsFinal);
      }
      const pageSource = convertNuxtPagesToSitemapEntries(await pagesPromise, {
        isI18nMapped,
        autoLastmod: config.autoLastmod,
        defaultLocale: nuxtI18nConfig.defaultLocale || "en",
        strategy: nuxtI18nConfig.strategy || "no_prefix",
        routesNameSeparator: nuxtI18nConfig.routesNameSeparator,
        normalisedLocales,
        filter: {
          include: serializeFilters(config.include || [], "@nuxtjs/sitemap"),
          exclude: serializeFilters(config.exclude || [], "@nuxtjs/sitemap")
        },
        autoI18n: !!resolvedAutoI18n
      });
      if (!pageSource.length) {
        pageSource.push(nuxt.options.app.baseURL || "/");
      }
      const allPrerenderedPaths = new Set(
        prerenderedRoutes2.filter(isValidPrerenderRoute).map((r) => r.route)
      );
      const pageSourceByPath = /* @__PURE__ */ new Map();
      for (const p of pageSource) {
        if (typeof p !== "string" && p.loc)
          pageSourceByPath.set(p.loc, p);
      }
      for (let i = 0; i < prerenderUrlsFinal.length; i++) {
        const entry = prerenderUrlsFinal[i];
        if (!entry || typeof entry === "string")
          continue;
        const pageEntry = pageSourceByPath.get(entry.loc);
        if (pageEntry && typeof pageEntry !== "string") {
          prerenderUrlsFinal[i] = defu(entry, pageEntry);
        }
      }
      const dedupedPageSource = pageSource.filter((p) => {
        const path = typeof p === "string" ? p : p.loc;
        return !allPrerenderedPaths.has(path);
      });
      if (!resolvedConfigUrls && config.urls) {
        const urls = await resolveUrls(config.urls, { path: "sitemap:urls", logger });
        if (urls.length) {
          userGlobalSources.push({
            context: {
              name: "sitemap:urls",
              description: "Set with the `sitemap.urls` config."
            },
            urls
          });
        }
        resolvedConfigUrls = true;
      }
      const globalSources = [
        ...userGlobalSources.map((s) => {
          if (typeof s === "string" || Array.isArray(s)) {
            return {
              sourceType: "user",
              fetch: s
            };
          }
          s.sourceType = "user";
          return s;
        }),
        ...(excludedAppSources === true ? [] : [
          ...appGlobalSources,
          {
            context: {
              name: "nuxt:pages",
              description: "Generated from your static page files.",
              tips: [
                "Can be disabled with `{ excludeAppSources: ['nuxt:pages'] }`."
              ]
            },
            urls: dedupedPageSource
          },
          {
            context: {
              name: "nuxt:route-rules",
              description: "Generated from your route rules config.",
              tips: [
                "Can be disabled with `{ excludeAppSources: ['nuxt:route-rules'] }`."
              ]
            },
            urls: routeRules2
          },
          {
            context: {
              name: "nuxt:prerender",
              description: "Generated at build time when prerendering.",
              tips: [
                "Can be disabled with `{ excludeAppSources: ['nuxt:prerender'] }`."
              ]
            },
            urls: prerenderUrlsFinal
          }
        ]).filter((s) => !excludedAppSources.includes(s.context.name) && (!!s.urls?.length || !!s.fetch)).map((s) => {
          s.sourceType = "app";
          return s;
        })
      ];
      return globalSources;
    };
    const extraSitemapModules = typeof config.sitemaps == "object" ? Object.keys(config.sitemaps).filter((n) => n !== "index") : [];
    const sitemapSources = {};
    const generateChildSources = async () => {
      for (const sitemapName of extraSitemapModules) {
        sitemapSources[sitemapName] = sitemapSources[sitemapName] || [];
        const definition = config.sitemaps[sitemapName];
        if (!sitemapSources[sitemapName].length) {
          if (definition.urls) {
            sitemapSources[sitemapName].push({
              context: {
                name: `sitemaps:${sitemapName}:urls`,
                description: "Set with the `sitemap.urls` config."
              },
              urls: await resolveUrls(definition.urls, { path: `sitemaps:${sitemapName}:urls`, logger })
            });
          }
          sitemapSources[sitemapName].push(
            ...(definition.sources || []).map((s) => {
              if (typeof s === "string" || Array.isArray(s)) {
                return {
                  sourceType: "user",
                  fetch: s
                };
              }
              s.sourceType = "user";
              return s;
            })
          );
        }
      }
      return sitemapSources;
    };
    nuxt.hooks.hook("nitro:config", (nitroConfig) => {
      nitroConfig.virtual = nitroConfig.virtual || {};
      if (!nitroConfig.virtual["#sitemap-virtual/read-sources.mjs"]) {
        nitroConfig.virtual["#sitemap-virtual/read-sources.mjs"] = `
export async function readSourcesFromFilesystem() {
  return null
}
`;
      }
      nitroConfig.virtual["#sitemap-virtual/global-sources.mjs"] = async () => {
        const globalSources = await generateGlobalSources();
        return `export const sources = ${JSON.stringify(globalSources, null, 4)}`;
      };
      nitroConfig.virtual[`#sitemap-virtual/child-sources.mjs`] = async () => {
        const childSources = await generateChildSources();
        return `export const sources = ${JSON.stringify(childSources, null, 4)}`;
      };
    });
    if (config.xsl === "/__sitemap__/style.xsl") {
      addServerHandler({
        route: config.xsl,
        handler: resolve("./runtime/server/routes/sitemap.xsl")
      });
      config.xsl = withBase(config.xsl, nuxt.options.app.baseURL);
      if (prerenderSitemap)
        addPrerenderRoutes(config.xsl);
    }
    addServerHandler({
      route: `/${config.sitemapName}`,
      handler: resolve(`${routesPath}/sitemap.xml`)
    });
    setupPrerenderHandler({ runtimeConfig, logger, generateGlobalSources, generateChildSources, prerenderSitemap });
    if (!config.zeroRuntime && !nuxt.options.dev && !nuxt.options._prepare) {
      const hasDynamicSource = (source) => typeof source === "string" || Array.isArray(source) || !!source.fetch;
      const globalHasFetch = (config.sources || []).some(hasDynamicSource);
      const sitemapsHaveFetch = typeof config.sitemaps === "object" && Object.values(config.sitemaps).some((s) => s && "sources" in s && (s.sources || []).some(hasDynamicSource));
      if (!globalHasFetch && !sitemapsHaveFetch)
        logger.info("No dynamic sources detected. Consider enabling `zeroRuntime` to reduce server bundle size. See https://nuxtseo.com/sitemap/guides/zero-runtime");
    }
  }
});

export { module$1 as default };
