import { tryUseNuxt, installModule, resolvePath, useNuxt } from '@nuxt/kit';
import { resolveSitePath, fixSlashes } from 'site-config-stack/urls';
import { env } from 'std-env';
import { createSiteConfigStack, SiteConfigPriority, envSiteConfig } from 'site-config-stack';
import { getNitroOrigin } from '../util.mjs';

async function initSiteConfig(nuxt = tryUseNuxt()) {
  if (!nuxt)
    return;
  let siteConfig = nuxt._siteConfig;
  if (siteConfig)
    return siteConfig;
  siteConfig = createSiteConfigStack();
  siteConfig.push({
    _context: "system",
    _priority: SiteConfigPriority.system,
    env: nuxt.options.envName || process.env.NODE_ENV
  });
  siteConfig.push({
    _context: "vendorEnv",
    _priority: SiteConfigPriority.vendor,
    url: [
      // vercel
      process.env.VERCEL_URL,
      process.env.NUXT_ENV_VERCEL_URL,
      // netlify
      process.env.URL,
      // cloudflare pages
      process.env.CF_PAGES_URL
    ].find((k) => Boolean(k)),
    name: [
      // vercel
      process.env.NUXT_ENV_VERCEL_GIT_REPO_SLUG,
      // netlify
      process.env.SITE_NAME
    ].find((k) => Boolean(k))
  });
  siteConfig.push({
    _context: "buildEnv",
    _priority: SiteConfigPriority.build,
    ...envSiteConfig(process.env || {})
  });
  nuxt._siteConfig = siteConfig;
  return siteConfig;
}
async function installNuxtSiteConfig(nuxt = tryUseNuxt()) {
  await installModule(await resolvePath("nuxt-site-config"));
  await initSiteConfig(nuxt);
}
function getSiteConfigStack(nuxt = tryUseNuxt()) {
  if (!nuxt)
    throw new Error("Nuxt context is missing.");
  if (!nuxt._siteConfig)
    throw new Error("Site config is not initialized. Make sure you are running your module after nuxt-site-config.");
  return nuxt._siteConfig;
}
function updateSiteConfig(input, nuxt = tryUseNuxt()) {
  const container = getSiteConfigStack(nuxt);
  return container.push(input);
}
function useSiteConfig(nuxt = tryUseNuxt()) {
  const container = getSiteConfigStack(nuxt);
  return container.get();
}

function withSiteTrailingSlash(path) {
  const siteConfig = useSiteConfig();
  return fixSlashes(siteConfig.trailingSlash, path);
}
function createSitePathResolver(options = {}, nuxt = useNuxt()) {
  const siteConfig = useSiteConfig();
  const nitroOrigin = getNitroOrigin();
  const canUseSiteUrl = (options.canonical !== false || env.prerender) && siteConfig.url;
  const nuxtBase = nuxt.options.app.baseURL || "/";
  return (path) => {
    return resolveSitePath(path, {
      ...options,
      siteUrl: canUseSiteUrl ? siteConfig.url : nitroOrigin,
      trailingSlash: siteConfig.trailingSlash,
      base: nuxtBase
    });
  };
}
function withSiteUrl(path, options = {}) {
  const siteConfig = useSiteConfig();
  if (!siteConfig.url && options.throwErrorOnMissingSiteUrl)
    throw new Error("Missing url in site config. Please add `{ site: { url: <url> } }` to nuxt.config.ts.");
  const nuxt = useNuxt();
  const base = nuxt.options.app.baseURL || "/";
  return resolveSitePath(path, {
    absolute: true,
    siteUrl: siteConfig.url || "",
    trailingSlash: siteConfig.trailingSlash,
    base,
    withBase: options.withBase
  });
}

export { installNuxtSiteConfig as a, useSiteConfig as b, createSitePathResolver as c, withSiteUrl as d, getSiteConfigStack as g, initSiteConfig as i, updateSiteConfig as u, withSiteTrailingSlash as w };
