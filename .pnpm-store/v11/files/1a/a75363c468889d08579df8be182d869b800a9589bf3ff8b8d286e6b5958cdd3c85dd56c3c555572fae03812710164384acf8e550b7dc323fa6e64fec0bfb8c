import { defu } from 'defu';
import { toRouteMatcher, createRouter } from 'radix3';
import { withoutTrailingSlash, parseURL, withoutBase } from 'ufo';

function withoutQuery(path) {
  const queryIndex = path.indexOf("?");
  return queryIndex === -1 ? path : path.slice(0, queryIndex);
}
function createNitroRouteRuleMatcher(runtimeConfig) {
  const { nitro, app } = runtimeConfig;
  const baseURL = app?.baseURL || "/";
  const _routeRulesMatcher = toRouteMatcher(
    createRouter({
      routes: Object.fromEntries(
        Object.entries(nitro?.routeRules || {}).map(([path, rules]) => [withoutTrailingSlash(path), rules])
      )
    })
  );
  return (pathOrUrl) => {
    const path = pathOrUrl[0] === "/" ? pathOrUrl : parseURL(pathOrUrl, baseURL).pathname;
    return defu({}, ..._routeRulesMatcher.matchAll(
      withoutBase(withoutTrailingSlash(withoutQuery(path)), baseURL)
    ).reverse());
  };
}
function normalizeNitroMatchedRouteRules(matchedRouteRules) {
  return Object.fromEntries(
    Object.entries(matchedRouteRules || {}).map(([key, rule]) => [key, rule.options])
  );
}

export { createNitroRouteRuleMatcher, normalizeNitroMatchedRouteRules, withoutQuery };
