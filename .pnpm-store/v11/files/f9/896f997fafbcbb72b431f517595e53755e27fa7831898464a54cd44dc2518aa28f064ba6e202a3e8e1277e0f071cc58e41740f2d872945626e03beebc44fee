import { createPatternMap } from "@nuxtjs/robots/util";
import { createNitroRouteRuleMatcher } from "nuxtseo-shared/server";
import { withoutTrailingSlash } from "ufo";
import { defineNitroPlugin, useRuntimeConfig } from "#nuxtseo/nitro";
import { useRuntimeConfigNuxtRobots } from "../composables/useRuntimeConfigNuxtRobots.js";
import { logger } from "../logger.js";
import { resolveRobotsTxtContext } from "../util.js";
const PRERENDER_NO_SSR_ROUTES = /* @__PURE__ */ new Set(["/index.html", "/200.html", "/404.html"]);
export default defineNitroPlugin(async (nitroApp) => {
  const { isNuxtContentV2, robotsDisabledValue, botDetection } = useRuntimeConfigNuxtRobots();
  if (botDetection !== false) {
    nitroApp._robotsPatternMap = createPatternMap();
  }
  nitroApp._robots = {};
  await resolveRobotsTxtContext(void 0, nitroApp);
  const nuxtContentUrls = /* @__PURE__ */ new Set();
  if (isNuxtContentV2) {
    let urls;
    try {
      urls = await (await nitroApp.localFetch("/__robots__/nuxt-content.json", {})).json();
    } catch (e) {
      logger.error("Failed to read robot rules from content files.", e);
    }
    if (urls && Array.isArray(urls) && urls.length) {
      urls.forEach((url) => nuxtContentUrls.add(withoutTrailingSlash(url)));
    }
  }
  if (nuxtContentUrls.size) {
    nitroApp._robots.nuxtContentUrls = nuxtContentUrls;
  }
  if (import.meta.prerender) {
    nitroApp.hooks.hook("render:html", async (ctx, { event }) => {
      nitroApp._robotsRuleMatcher ||= createNitroRouteRuleMatcher(useRuntimeConfig(event));
      const routeOptions = nitroApp._robotsRuleMatcher(event.path);
      const isIsland = process.env.NUXT_COMPONENT_ISLANDS && event.path.startsWith("/__nuxt_island");
      const noSSR = !!process.env.NUXT_NO_SSR || event.context.nuxt?.noSSR || routeOptions.ssr === false && !isIsland || (import.meta.prerender ? PRERENDER_NO_SSR_ROUTES.has(event.path) : false);
      if (noSSR) {
        let rule = event.context.robots?.rule;
        if (event.path === "/404.html")
          rule = robotsDisabledValue;
        if (rule)
          ctx.head.push(`<meta name="robots" content="${rule}" />`);
      }
    });
  }
});
