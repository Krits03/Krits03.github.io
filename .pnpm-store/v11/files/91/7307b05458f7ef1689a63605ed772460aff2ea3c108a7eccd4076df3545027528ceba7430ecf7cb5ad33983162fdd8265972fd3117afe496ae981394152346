import { normalizeNitroMatchedRouteRules } from "nuxtseo-shared/server";
import { getNitroRouteRules, hasMatchedRouteRules } from "#nuxt-site-config/route-rules";
export function getSiteRouteRules(event) {
  const nitroRouteRules = getNitroRouteRules(event);
  const routeRules = hasMatchedRouteRules ? normalizeNitroMatchedRouteRules(nitroRouteRules) : nitroRouteRules;
  return {
    site: routeRules.site,
    // Nitro 3 removes matched false rules, while Nuxt treats a missing ssr rule as no-SSR.
    ssr: routeRules.ssr ?? false
  };
}
