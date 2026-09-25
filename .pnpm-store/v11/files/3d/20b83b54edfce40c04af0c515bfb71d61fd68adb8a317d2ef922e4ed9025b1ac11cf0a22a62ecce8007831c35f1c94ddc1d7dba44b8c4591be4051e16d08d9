import { createError, injectHead, useError, useNuxtApp, useRequestEvent, useRoute, useState } from "nuxt/app";
import { toValue } from "vue";
import { clientProcessOgImageOptions } from "../client-utils.js";
import { createOgImageMeta, getOgImagePath, setHeadOgImagePrebuilt, useOgImageRuntimeConfig } from "../utils.js";
export function defineOgImageRaw(_options = {}) {
  const nuxtApp = useNuxtApp();
  const route = useRoute();
  const basePath = route.path || "/";
  if (import.meta.dev && import.meta.server) {
    useState(`og-image:ssr-exists:${basePath}`, () => false).value = true;
  }
  if (!import.meta.server) {
    if (import.meta.dev && nuxtApp.isHydrating) {
      const state = useState(`og-image:ssr-exists:${basePath}`, () => false);
      if (!state.value && !useError().value) {
        throw createError({ message: "You are using a defineOgImage() function in a client-only context. You must call this function within your root component setup, see https://github.com/nuxt-modules/og-image/pull/293." });
      }
    }
    if (nuxtApp.isHydrating)
      return [];
    return clientProcessOgImageOptions(_options, route, basePath);
  }
  const paths = [];
  if (Array.isArray(_options)) {
    for (const opt of _options) {
      const path2 = useProcessOgImageOptions(opt, nuxtApp, route, basePath);
      if (path2)
        paths.push(path2);
    }
    return paths;
  }
  const path = useProcessOgImageOptions(_options, nuxtApp, route, basePath);
  if (path)
    paths.push(path);
  return paths;
}
function useProcessOgImageOptions(_options, nuxtApp, route, basePath) {
  const { defaults } = useOgImageRuntimeConfig();
  const options = toValue(_options);
  if (options === false) {
    return;
  }
  if (nuxtApp.ssrContext?.event.context._nitro?.routeRules?.ogImage === false) {
    nuxtApp.ssrContext._ogImageInstance?.dispose();
    nuxtApp.ssrContext._ogImageDevtoolsInstance?.dispose();
    nuxtApp.ssrContext._ogImageInstance = void 0;
    nuxtApp.ssrContext._ogImagePayloads = [];
    if (import.meta.prerender) {
      const event = useRequestEvent(nuxtApp);
      if (event?.context._ogImagePrerenderPaths)
        event.context._ogImagePrerenderPaths.clear();
    }
    return;
  }
  const validOptions = options;
  if (validOptions.width)
    validOptions.width = toValue(validOptions.width);
  if (validOptions.height)
    validOptions.height = toValue(validOptions.height);
  if (validOptions.alt)
    validOptions.alt = toValue(validOptions.alt);
  if (validOptions.url)
    validOptions.url = toValue(validOptions.url);
  if (validOptions.props) {
    validOptions.props = { ...validOptions.props };
    for (const key in validOptions.props) {
      validOptions.props[key] = toValue(validOptions.props[key]);
    }
  }
  for (const key in defaults) {
    if (validOptions[key] === void 0)
      validOptions[key] = defaults[key];
  }
  let head;
  if (import.meta.server) {
    try {
      head = injectHead();
    } catch (e) {
      if (import.meta.dev)
        console.warn("[nuxt-og-image] Failed to inject head for OG image metadata generation.", e);
    }
  }
  if (route.query)
    validOptions._query = route.query;
  if (validOptions.url) {
    setHeadOgImagePrebuilt(validOptions);
    return toValue(validOptions.url);
  }
  const { path, hash } = getOgImagePath(basePath, validOptions);
  if (hash) {
    validOptions._hash = hash;
  }
  createOgImageMeta(path, validOptions, nuxtApp.ssrContext, basePath, head);
  if (import.meta.prerender) {
    const event = useRequestEvent(nuxtApp);
    if (!event.context._ogImagePrerenderPaths)
      event.context._ogImagePrerenderPaths = /* @__PURE__ */ new Map();
  }
  return path;
}
