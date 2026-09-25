import { useNuxtApp } from "#imports";
import { defu } from "defu";
export function useLazyComponentTracking(components = []) {
  const nuxtApp = useNuxtApp();
  if (!nuxtApp.payload.__hints?.lazyHydrationState) {
    nuxtApp.payload.__hints = defu(nuxtApp.payload.__hints, {
      lazyHydrationState: {
        directImports: /* @__PURE__ */ new Map(),
        hasReported: false,
        pageLoaded: false
      }
    });
  }
  const state = nuxtApp.payload.__hints.lazyHydrationState;
  for (const comp of components) {
    state.directImports.set(comp.componentName, comp);
  }
  return state;
}
export function __wrapMainComponent(component, imports = []) {
  const originalSetup = component.setup;
  component.setup = (props, ctx) => {
    useLazyComponentTracking(imports);
    return originalSetup ? originalSetup(props, ctx) : void 0;
  };
  return component;
}
export function __wrapImportedComponent(component, componentName, importSource, importedBy) {
  if (component && component.name === "AsyncComponentWrapper") {
    return component;
  }
  const originalSetup = component.setup;
  component.setup = (props, ctx) => {
    const state = useLazyComponentTracking();
    if (state) {
      if (!state.directImports.has(componentName)) {
        state.directImports.set(componentName, {
          componentName,
          importSource,
          importedBy,
          rendered: false
        });
      }
      const info = state.directImports.get(componentName);
      if (info) {
        info.rendered = true;
      }
    }
    return originalSetup ? originalSetup(props, ctx) : void 0;
  };
  return component;
}
