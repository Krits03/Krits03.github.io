import { matchPathToRule, normaliseRobotsRouteRule } from "@nuxtjs/robots/util";
import { resolveLocaleFromRoute } from "nuxtseo-shared/i18n-runtime";
import { createNitroRouteRuleMatcher } from "nuxtseo-shared/server";
import { withoutTrailingSlash } from "ufo";
import { getRequestHeader } from "#nuxtseo/h3";
import { useNitroApp, useRuntimeConfig } from "#nuxtseo/nitro";
import { getSiteRobotConfig } from "./getSiteRobotConfig.js";
import { useRuntimeConfigNuxtRobots } from "./useRuntimeConfigNuxtRobots.js";
const i18nStrategies = /* @__PURE__ */ new Set(["no_prefix", "prefix_except_default", "prefix", "prefix_and_default"]);
function parseRuntimeI18nConfig(input) {
  if (!input || typeof input !== "object")
    return null;
  const config = input;
  if (!Array.isArray(config.locales))
    return null;
  const locales = config.locales.flatMap((locale) => {
    const code = typeof locale === "string" ? locale : locale && typeof locale === "object" && typeof locale.code === "string" ? locale.code : null;
    return code ? [{ code, hreflang: code }] : [];
  });
  if (!locales.length)
    return null;
  const defaultLocale = typeof config.defaultLocale === "string" ? config.defaultLocale : locales[0].code;
  const strategy = typeof config.strategy === "string" && i18nStrategies.has(config.strategy) ? config.strategy : "prefix";
  return { defaultLocale, locales, strategy };
}
export function getPathRobotConfig(e, options) {
  const runtimeConfig = useRuntimeConfig(e);
  const { robotsDisabledValue, robotsEnabledValue, isNuxtContentV2 } = useRuntimeConfigNuxtRobots(e);
  if (!options?.skipSiteIndexable) {
    if (!getSiteRobotConfig(e).indexable) {
      return {
        rule: robotsDisabledValue,
        indexable: false,
        debug: {
          source: "Site Config"
        }
      };
    }
  }
  const path = options?.path || e.path;
  let userAgent = options?.userAgent;
  if (!userAgent) {
    try {
      userAgent = getRequestHeader(e, "User-Agent");
    } catch {
    }
  }
  const nitroApp = useNitroApp();
  const groups = [
    // run explicit user agent matching first
    ...nitroApp._robots.ctx.groups.filter((g) => {
      if (userAgent) {
        return g.userAgent.some((ua) => !!ua && userAgent.toLowerCase().includes(ua.toLowerCase()));
      }
      return false;
    }),
    // run wildcard matches second
    ...nitroApp._robots.ctx.groups.filter((g) => g.userAgent.includes("*"))
  ];
  for (const group of groups) {
    if (!options?.skipSiteIndexable && group._indexable === false) {
      return {
        indexable: false,
        rule: robotsDisabledValue,
        debug: {
          source: "/robots.txt",
          line: JSON.stringify(group)
        }
      };
    }
    const rules = options?.skipSiteIndexable ? (group._rules || []).filter((r) => r.pattern !== "/") : group._rules || [];
    const robotsTxtRule = matchPathToRule(path, rules);
    if (robotsTxtRule) {
      if (!robotsTxtRule.allow) {
        return {
          indexable: false,
          rule: robotsDisabledValue,
          debug: {
            source: "/robots.txt",
            line: `Disallow: ${robotsTxtRule.pattern}`
          }
        };
      }
      break;
    }
  }
  if (isNuxtContentV2 && nitroApp._robots?.nuxtContentUrls?.has(withoutTrailingSlash(path))) {
    return {
      indexable: false,
      rule: robotsDisabledValue,
      debug: {
        source: "Nuxt Content"
      }
    };
  }
  const { pageMetaRobots } = useRuntimeConfigNuxtRobots(e);
  const pageMetaRule = pageMetaRobots?.[withoutTrailingSlash(path)];
  if (typeof pageMetaRule !== "undefined") {
    const normalised = normaliseRobotsRouteRule({ robots: pageMetaRule });
    if (normalised && (typeof normalised.allow !== "undefined" || typeof normalised.rule !== "undefined")) {
      return {
        indexable: normalised.allow ?? false,
        rule: normalised.rule || (normalised.allow ? robotsEnabledValue : robotsDisabledValue),
        debug: {
          source: "Page Meta"
        }
      };
    }
  }
  nitroApp._robotsRuleMatcher = nitroApp._robotsRuleMatcher || createNitroRouteRuleMatcher(runtimeConfig);
  let robotRouteRules = nitroApp._robotsRuleMatcher(path);
  let routeRulesPath = path;
  const i18nConfig = parseRuntimeI18nConfig(runtimeConfig.public?.i18n);
  if (i18nConfig && typeof robotRouteRules.robots === "undefined") {
    const resolvedRoute = resolveLocaleFromRoute(routeRulesPath, i18nConfig);
    if (resolvedRoute.basePath !== routeRulesPath) {
      routeRulesPath = resolvedRoute.basePath;
      robotRouteRules = nitroApp._robotsRuleMatcher(routeRulesPath);
    }
  }
  const routeRules = normaliseRobotsRouteRule(robotRouteRules);
  if (routeRules && (typeof routeRules.allow !== "undefined" || typeof routeRules.rule !== "undefined")) {
    return {
      indexable: routeRules.allow ?? false,
      rule: routeRules.rule || (routeRules.allow ? robotsEnabledValue : robotsDisabledValue),
      debug: {
        source: "Route Rules"
      }
    };
  }
  return {
    indexable: true,
    rule: robotsEnabledValue
  };
}
