import { defineNuxtPlugin, useNuxtApp, useRoute } from "#imports";
import { defu } from "defu";
import { useLazyComponentTracking } from "./composables.js";
import { logger, LAZY_LOAD_ROUTE } from "./utils.js";
import { isFeatureDevtoolsEnabled } from "../core/features.js";
export default defineNuxtPlugin({
  name: "@nuxt/hints:lazy-load",
  dependsOn: ["nuxt:router"],
  setup() {
    const nuxtApp = useNuxtApp();
    nuxtApp.payload.__hints = defu(nuxtApp.payload.__hints, {
      lazyComponents: []
    });
    if (import.meta.client) {
      const state = useLazyComponentTracking();
      if (!state) return;
      nuxtApp.hook("app:suspense:resolve", () => {
        if (state.hasReported || state.pageLoaded) return;
        state.pageLoaded = true;
        setTimeout(() => {
          nuxtApp.runWithContext(() => checkAndReport(state));
        }, 500);
      });
    }
  }
});
function checkAndReport(state) {
  if (state.hasReported) return;
  state.hasReported = true;
  const suggestions = [];
  for (const [_, info] of state.directImports) {
    if (!info.rendered) {
      suggestions.push(info);
    }
  }
  if (suggestions.length > 0) {
    reportSuggestions(suggestions);
  }
}
function reportSuggestions(suggestions) {
  const route = useRoute();
  const nuxtApp = useNuxtApp();
  nuxtApp.payload.__hints.lazyComponents = suggestions;
  logger.info(
    `${suggestions.length} component has not been rendered in SSR nor rendered at hydration time. Consider lazy loading it:
`
  );
  for (const suggestion of suggestions) {
    const lazyName = `Lazy${suggestion.componentName}`;
    logger.info(
      `${suggestion.componentName} \u2192 Use <${lazyName}> or \`defineAsyncComponent\` instead
  Imported from: ${suggestion.importSource}
  Used in: ${suggestion.importedBy}`
    );
  }
  if (suggestions.length && isFeatureDevtoolsEnabled("lazyLoad")) {
    const payload = {
      id: `${encodeURIComponent(route.path)}-${Date.now()}`,
      route: route.path,
      state: {
        pageLoaded: true,
        hasReported: true,
        directImports: suggestions
      }
    };
    $fetch(LAZY_LOAD_ROUTE, {
      method: "POST",
      body: payload
    }).catch((err) => {
      logger.warn("Failed to send lazy-load data to server:", err);
    });
  }
}
