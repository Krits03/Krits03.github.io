import { createNitroRouteRuleMatcher as createRouteRuleMatcher } from "nuxtseo-shared/server";
import { fetchWithEvent, useRuntimeConfig } from "#nuxtseo/nitro";
import { getIslandHash } from "#og-image/island-hash";
export function fetchIsland(e, component, props, timeout) {
  const hashId = getIslandHash({ name: component, props });
  const signal = timeout ? AbortSignal.timeout(timeout) : void 0;
  return fetchWithEvent(e, `/__nuxt_island/${component}_${hashId}.json`, {
    params: {
      props: JSON.stringify(props)
    },
    timeout,
    signal
  });
}
export function createNitroRouteRuleMatcher() {
  return createRouteRuleMatcher(useRuntimeConfig());
}
