import { pathToFileURL } from 'node:url';
import { getNuxtVersion, addTypeTemplate, useNuxt, useLogger, resolveModule, directoryToURL, createResolver, addTemplate, loadNuxtModuleInstance, hasNuxtModule, tryUseNuxt, hasNuxtModuleCompatibility } from '@nuxt/kit';
import { relative, dirname } from 'pathe';
import { resolvePackageJSON, readPackageJSON } from 'pkg-types';
import { provider, env } from 'std-env';

const NITRO_RUNTIME_MODULE = "#nuxtseo/nitro";
const H3_RUNTIME_MODULE = "#nuxtseo/h3";
const OFETCH_RUNTIME_MODULE = "#nuxtseo/ofetch";
const TYPE_TEMPLATE_FILENAME = "types/nuxtseo-nitro.d.ts";
const legacySetupMarker = Symbol.for("nuxtseo:nitro-runtime-compatibility");
const typeSetupMarker = Symbol.for("nuxtseo:nitro-runtime-compatibility:request-context-types");
const runtimeSetupMarker = Symbol.for("nuxtseo:nitro-runtime-compatibility:request-context");
const nitroV2Compatibility = {
  _tag: "nitro-v2",
  eventContextModule: "h3",
  eventContextType: "H3EventContext",
  eventType: `import('h3').H3Event`,
  nitroTypesModule: "nitropack"
};
const nitroV3Compatibility = {
  _tag: "nitro-v3",
  eventContextModule: "srvx",
  eventContextType: "ServerRequestContext",
  eventType: `import('nitro/h3').H3Event`,
  nitroTypesModule: "nitro/types"
};
const nitroV2Runtime = `export {
  defineNitroPlugin,
  useNitroApp,
  useEvent,
  useRuntimeConfig,
  defineCachedFunction,
  defineCachedEventHandler,
  useStorage,
  defineTask,
  runTask,
} from 'nitropack/runtime'
export function fetchWithEvent(event, request, options) {
  return event.$fetch(request, options)
}
export function fetchRawWithEvent(event, request, init) {
  return event.fetch(request, init)
}
`;
const nitroV2RuntimeTypes = `export {
  defineNitroPlugin,
  useNitroApp,
  useEvent,
  useRuntimeConfig,
  defineCachedFunction,
  defineCachedEventHandler,
  useStorage,
  defineTask,
  runTask,
} from 'nitropack/runtime'
export function fetchWithEvent<T>(event: import('h3').H3Event, request: import('ofetch').FetchRequest, options?: import('ofetch').FetchOptions): Promise<T>
export function fetchRawWithEvent(event: import('h3').H3Event, request: RequestInfo | URL, init?: RequestInit): Promise<Response>
`;
const nitroV3Runtime = `import { createFetch } from '${OFETCH_RUNTIME_MODULE}'
import { fetchWithEvent as fetchH3WithEvent, getProxyRequestHeaders } from 'nitro/h3'
import { useNitroApp as _useNitroApp } from 'nitro/app'
export { definePlugin as defineNitroPlugin } from 'nitro'
export { useNitroApp } from 'nitro/app'
export { useRequest as useEvent } from 'nitro/context'
import { useRuntimeConfig as _useRuntimeConfig } from 'nitro/runtime-config'
export function useRuntimeConfig(_event) { return _useRuntimeConfig() }
export { defineCachedFunction, defineCachedHandler as defineCachedEventHandler } from 'nitro/cache'
export { useStorage } from 'nitro/storage'
export { defineTask, runTask } from 'nitro/task'
function fetchRaw(event, input, init) {
  if (typeof input !== 'string' || !input.startsWith('/'))
    return fetchH3WithEvent(event, input, init)
  const headers = new Headers(getProxyRequestHeaders(event, { host: true }))
  for (const [name, value] of new Headers(init?.headers))
    headers.set(name, value)
  const request = new Request(new URL(input, event.url), { ...init, headers })
  request.runtime = event.req.runtime
  request.waitUntil = event.req.waitUntil
  request.ip = event.req.ip
  return _useNitroApp().fetch(request)
}
export function fetchRawWithEvent(event, request, init) {
  return fetchRaw(event, request, init)
}
export function fetchWithEvent(event, request, options) {
  const localFetch = createFetch({
    fetch: (input, init) => fetchRaw(event, input, init),
  })
  return localFetch(request, options)
}
`;
const nitroV3RuntimeTypes = `export { definePlugin as defineNitroPlugin } from 'nitro'
export { useNitroApp } from 'nitro/app'
export { useRequest as useEvent } from 'nitro/context'
export function useRuntimeConfig(event?: import('nitro/h3').H3Event): ReturnType<typeof import('nitro/runtime-config').useRuntimeConfig>
export { defineCachedFunction, defineCachedHandler as defineCachedEventHandler } from 'nitro/cache'
export { useStorage } from 'nitro/storage'
export { defineTask, runTask } from 'nitro/task'
export function fetchWithEvent<T>(event: import('nitro/h3').H3Event, request: import('ofetch').FetchRequest, options?: import('ofetch').FetchOptions): Promise<T>
export function fetchRawWithEvent(event: import('nitro/h3').H3Event, request: RequestInfo | URL, init?: RequestInit): Promise<Response>
`;
function indent(value, spaces) {
  const padding = " ".repeat(spaces);
  return value.split("\n").map((line) => `${padding}${line}`).join("\n");
}
function renderInterface(name, contents) {
  if (!contents?.trim())
    return void 0;
  return `  interface ${name} {
${indent(contents.trim(), 4)}
  }`;
}
function renderRuntimeDeclarations(compatibility) {
  const nitroRuntime = compatibility._tag === "nitro-v3" ? nitroV3RuntimeTypes : nitroV2RuntimeTypes;
  const h3Runtime = compatibility._tag === "nitro-v3" ? `export * from 'nitro/h3'
` : `export * from 'h3'
`;
  return `declare module '${NITRO_RUNTIME_MODULE}' {
${indent(nitroRuntime.trim(), 2)}
}

declare module '${H3_RUNTIME_MODULE}' {
${indent(h3Runtime.trim(), 2)}
}
`;
}
function resolveRuntimeModule(nuxt, id) {
  try {
    return {
      _tag: "resolved",
      path: resolveModule(id, {
        url: [...nuxt.options.modulesDir.map(directoryToURL), new URL(import.meta.url)]
      })
    };
  } catch (cause) {
    return { _tag: "unresolved", cause };
  }
}
function applyNitroRuntimeCompatibility(nuxt, compatibility, reportResolutionFailure = false) {
  const nuxtOptions = nuxt.options;
  const nitroOptions = nuxtOptions.nitro ||= {};
  nitroOptions.alias ||= {};
  nitroOptions.externals ||= {};
  nitroOptions.externals.inline ||= [];
  nitroOptions.virtual ||= {};
  if (!nitroOptions.externals.inline.includes("nuxtseo-shared"))
    nitroOptions.externals.inline.push("nuxtseo-shared");
  const h3RuntimeModule = compatibility._tag === "nitro-v3" ? "nitro/h3" : "h3";
  nitroOptions.alias[H3_RUNTIME_MODULE] = h3RuntimeModule;
  const h3Resolution = resolveRuntimeModule(nuxt, h3RuntimeModule);
  if (h3Resolution._tag === "resolved") {
    nitroOptions.typescript ||= {};
    nitroOptions.typescript.tsConfig ||= {};
    nitroOptions.typescript.tsConfig.compilerOptions ||= {};
    nitroOptions.typescript.tsConfig.compilerOptions.paths ||= {};
    nitroOptions.typescript.tsConfig.compilerOptions.paths[H3_RUNTIME_MODULE] = [h3Resolution.path];
  } else if (reportResolutionFailure) {
    useLogger("nuxtseo-shared").warn(
      `Could not resolve Nitro runtime module '${h3RuntimeModule}'. Generated server types may be incomplete.`,
      h3Resolution.cause
    );
  }
  if (compatibility._tag === "nitro-v3")
    nitroOptions.alias[OFETCH_RUNTIME_MODULE] = resolveModule("ofetch", { url: new URL(import.meta.url) });
  nitroOptions.virtual[NITRO_RUNTIME_MODULE] = compatibility._tag === "nitro-v3" ? nitroV3Runtime : nitroV2Runtime;
}
function renderNitroTypeAugmentations(compatibility, augmentations) {
  const nitroInterfaces = [
    renderInterface("NitroRouteRules", augmentations.routeRules),
    renderInterface("NitroRouteConfig", augmentations.routeConfig),
    renderInterface("NitroRuntimeHooks", augmentations.runtimeHooks),
    ...Object.entries(augmentations.nitroInterfaces || {}).map(([name, contents]) => renderInterface(name, contents))
  ].filter((value) => Boolean(value));
  const declarations = [];
  if (nitroInterfaces.length) {
    const nitroTypeModules = compatibility._tag === "nitro-v2" ? ["nitropack", "nitropack/types"] : [compatibility.nitroTypesModule];
    declarations.push(...nitroTypeModules.map((module) => `declare module '${module}' {
${nitroInterfaces.join("\n")}
}`));
  }
  if (augmentations.eventContext?.trim()) {
    declarations.push(`declare module '${compatibility.eventContextModule}' {
${renderInterface(compatibility.eventContextType, augmentations.eventContext)}
}`);
  }
  return declarations.join("\n\n");
}
function setupNitroRuntimeCompatibility(nuxt = useNuxt()) {
  const major = Number.parseInt(getNuxtVersion(nuxt), 10);
  const compatibility = major >= 5 ? nitroV3Compatibility : nitroV2Compatibility;
  applyNitroRuntimeCompatibility(nuxt, compatibility);
  const nuxtWithLegacyMarker = nuxt;
  nuxtWithLegacyMarker[legacySetupMarker] = true;
  const nuxtWithRuntimeMarker = nuxt;
  if (!nuxtWithRuntimeMarker[runtimeSetupMarker]) {
    nuxtWithRuntimeMarker[runtimeSetupMarker] = true;
    nuxt.hooks.hookOnce("modules:done", () => applyNitroRuntimeCompatibility(nuxt, compatibility, true));
  }
  const nuxtWithTypeMarker = nuxt;
  if (!nuxtWithTypeMarker[typeSetupMarker]) {
    nuxtWithTypeMarker[typeSetupMarker] = true;
    addTypeTemplate({
      filename: TYPE_TEMPLATE_FILENAME,
      getContents: async () => renderRuntimeDeclarations(compatibility)
    }, { nitro: true, nuxt: true });
  }
  return compatibility;
}

function normalizePackageUrl(rootDir) {
  const url = rootDir.startsWith("file:") ? rootDir : pathToFileURL(rootDir.endsWith("/") ? rootDir : `${rootDir}/`).href;
  return url.endsWith("/") ? url : `${url}/`;
}
const NUXT_SEO_MODULES = /* @__PURE__ */ new Set([
  "@nuxtjs/robots",
  "@nuxtjs/sitemap",
  "nuxt-og-image",
  "nuxt-schema-org",
  "nuxt-seo-utils",
  "nuxt-link-checker",
  "nuxt-site-config",
  "nuxt-skew-protection",
  "nuxt-ai-ready"
]);
function detectNuxtSeoModules(nuxt = useNuxt()) {
  return nuxt.options._installedModules.filter((m) => m.meta?.name && NUXT_SEO_MODULES.has(m.meta.name)).map((m) => ({
    name: m.meta.name,
    version: m.meta.version,
    entryPath: m.entryPath
  }));
}
function useModuleLogger(name, options, nuxt = useNuxt()) {
  const logger = useLogger(name);
  logger.level = options.debug || nuxt.options.debug ? 4 : 3;
  return logger;
}
const autodetectableProviders = {
  azure_static: "azure",
  cloudflare_pages: "cloudflare-pages",
  netlify: "netlify",
  stormkit: "stormkit",
  vercel: "vercel",
  cleavr: "cleavr",
  stackblitz: "stackblitz"
};
const autodetectableStaticProviders = {
  netlify: "netlify-static",
  vercel: "vercel-static"
};
function detectTarget(options = {}) {
  return options?.static ? autodetectableStaticProviders[provider] : autodetectableProviders[provider];
}
function resolveNitroPreset(nitroConfig) {
  nitroConfig = nitroConfig || tryUseNuxt()?.options?.nitro;
  if (provider === "stackblitz" || provider === "codesandbox")
    return provider;
  let preset;
  if (nitroConfig && nitroConfig?.preset)
    preset = nitroConfig.preset;
  if (!preset)
    preset = env.NITRO_PRESET || env.SERVER_PRESET || detectTarget() || "node-server";
  return preset.replaceAll("_", "-");
}
async function getNuxtModuleOptions(module, nuxt = useNuxt()) {
  const moduleMeta = (typeof module === "string" ? { name: module } : await module.getMeta?.()) || {};
  const { nuxtModule } = await loadNuxtModuleInstance(module, nuxt);
  let moduleEntry;
  for (const m of nuxt.options.modules) {
    if (Array.isArray(m) && m.length >= 2) {
      const _module = m[0];
      const _moduleEntryName = typeof _module === "string" ? _module : (await _module.getMeta?.())?.name || "";
      if (_moduleEntryName === moduleMeta.name)
        moduleEntry = m;
    }
  }
  let inlineOptions = {};
  if (moduleEntry)
    inlineOptions = moduleEntry[1];
  if (nuxtModule.getOptions)
    return nuxtModule.getOptions(inlineOptions, nuxt);
  return inlineOptions;
}
function isNuxtGenerate(nuxt = useNuxt()) {
  const nitroOptions = nuxt.options.nitro;
  return nitroOptions?.static || nuxt.options._generate || [
    "static",
    "github-pages"
  ].includes(resolveNitroPreset(nitroOptions));
}
function extendTypes(module, template) {
  const nuxt = useNuxt();
  const { resolve } = createResolver(import.meta.url);
  addTemplate({
    filename: `module/${module}.d.ts`,
    getContents: async () => {
      const typesPath = relative(resolve(nuxt.options.rootDir, nuxt.options.buildDir, "module"), resolve("runtime/types"));
      const s = await template({ typesPath });
      return `// Generated by ${module}
${s}
export {}
`;
    }
  });
  nuxt.hooks.hook("prepare:types", ({ references }) => {
    references.push({ path: resolve(nuxt.options.buildDir, `module/${module}.d.ts`) });
  });
}
function createPagesPromise(nuxt = useNuxt()) {
  return new Promise((resolve) => {
    nuxt.hooks.hook("modules:done", () => {
      if (typeof nuxt.options.pages === "boolean" && nuxt.options.pages === false || typeof nuxt.options.pages === "object" && !nuxt.options.pages.enabled) {
        return resolve([]);
      }
      nuxt.hook("pages:resolved", (pages) => resolve(pages));
    });
  });
}
function createNitroPromise(nuxt = useNuxt()) {
  return new Promise((resolve) => {
    nuxt.hooks.hook("nitro:init", (nitro) => resolve(nitro));
  });
}
async function resolveNuxtContentVersion() {
  if (!hasNuxtModule("@nuxt/content"))
    return false;
  if (await hasNuxtModuleCompatibility("@nuxt/content", "^3"))
    return { version: 3 };
  if (await hasNuxtModuleCompatibility("@nuxt/content", "^2"))
    return { version: 2 };
  return false;
}
async function resolvePackageMajor(id, rootDir) {
  const url = normalizePackageUrl(rootDir);
  const version = await readPackageJSON(id, { url }).then((pkg) => pkg.version).catch(() => {
    return void 0;
  });
  const major = version ? Number.parseInt(version, 10) : Number.NaN;
  return Number.isFinite(major) ? major : void 0;
}
async function resolveHostUnheadMajor(rootDir) {
  const rootUrl = normalizePackageUrl(rootDir);
  const searchUrls = [];
  for (const id of ["@nuxt/nitro-server", "nuxt"]) {
    const pkgJson = await resolvePackageJSON(id, { url: rootUrl }).catch(() => {
      return void 0;
    });
    if (pkgJson)
      searchUrls.push(`${dirname(pkgJson)}/`);
  }
  searchUrls.push(rootUrl);
  for (const id of ["@unhead/vue", "unhead"]) {
    for (const url of searchUrls) {
      const major = await resolvePackageMajor(id, url);
      if (major === 2)
        return 2;
      if (major !== void 0 && major >= 3)
        return 3;
    }
  }
  return 3;
}
const COMARK_CONTENT_MODULE = "@harlan-zw/comark-content";
const COMARK_CONTENT_MINIMUM = [0, 1, 2];
async function comarkSatisfiesMinimum(nuxt) {
  const pkg = await readPackageJSON(COMARK_CONTENT_MODULE, { url: normalizePackageUrl(nuxt.options.rootDir) }).catch(() => {
    return null;
  });
  const parts = pkg?.version?.split(".").map((part) => Number.parseInt(part, 10));
  if (!parts || parts.length < 3 || parts.some((part) => !Number.isFinite(part)))
    return false;
  for (const [index, minimum] of COMARK_CONTENT_MINIMUM.entries()) {
    if (parts[index] !== minimum)
      return parts[index] > minimum;
  }
  return true;
}
async function resolveContentProvider(nuxt = useNuxt()) {
  const nuxtContent = await resolveNuxtContentVersion();
  if (nuxtContent)
    return { _tag: "NuxtContent", version: nuxtContent.version };
  if (hasNuxtModule(COMARK_CONTENT_MODULE, nuxt) && await comarkSatisfiesMinimum(nuxt))
    return { _tag: "Comark" };
  return { _tag: "None" };
}
function hasContentFileHooks(provider2) {
  return provider2._tag === "Comark" || provider2._tag === "NuxtContent" && provider2.version === 3;
}
function setupContentRuntime(provider2, nuxt = useNuxt()) {
  const shim = provider2._tag === "Comark" ? "comark" : provider2._tag === "NuxtContent" && provider2.version === 3 ? "nuxt-content-v3" : "none";
  const resolver = createResolver(import.meta.url);
  const nitro = nuxt.options.nitro ??= {};
  nitro.alias ??= {};
  nitro.alias["#nuxtseo/content"] = resolver.resolve(`./runtime/content/${shim}`);
  nitro.externals ??= {};
  nitro.externals.inline ??= [];
  nitro.externals.inline.push(resolver.resolve("./runtime/content/"));
}

export { COMARK_CONTENT_MODULE, createNitroPromise, createPagesPromise, detectNuxtSeoModules, detectTarget, extendTypes, getNuxtModuleOptions, hasContentFileHooks, isNuxtGenerate, renderNitroTypeAugmentations, resolveContentProvider, resolveHostUnheadMajor, resolveNitroPreset, resolveNuxtContentVersion, resolvePackageMajor, setupContentRuntime, setupNitroRuntimeCompatibility, useModuleLogger };
