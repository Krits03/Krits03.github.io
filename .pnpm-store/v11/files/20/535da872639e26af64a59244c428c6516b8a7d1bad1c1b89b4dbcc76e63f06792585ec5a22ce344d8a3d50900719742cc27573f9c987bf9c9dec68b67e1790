import { Nuxt } from '@nuxt/schema';
import { Nitro } from 'nitropack';
import { NitroConfig } from 'nitropack/types';
import { NuxtPage, NuxtModule } from 'nuxt/schema';
import { useLogger } from '@nuxt/kit';

type NitroRuntimeCompatibility = {
    _tag: 'nitro-v2';
    eventContextModule: 'h3';
    eventContextType: 'H3EventContext';
    eventType: `import('h3').H3Event`;
    nitroTypesModule: 'nitropack';
} | {
    _tag: 'nitro-v3';
    eventContextModule: 'srvx';
    eventContextType: 'ServerRequestContext';
    eventType: `import('nitro/h3').H3Event`;
    nitroTypesModule: 'nitro/types';
};
interface NitroTypeAugmentations {
    eventContext?: string;
    nitroInterfaces?: Record<string, string>;
    routeConfig?: string;
    routeRules?: string;
    runtimeHooks?: string;
}
declare function renderNitroTypeAugmentations(compatibility: NitroRuntimeCompatibility, augmentations: NitroTypeAugmentations): string;
declare function setupNitroRuntimeCompatibility(nuxt?: Nuxt): NitroRuntimeCompatibility;

interface NuxtSeoModuleDetection {
    name: string;
    version?: string;
    entryPath?: string;
    features?: Record<string, boolean | string | number>;
}
/**
 * Detect all installed Nuxt SEO modules from `nuxt.options._installedModules`.
 * No self-registration needed; modules are discovered automatically.
 */
declare function detectNuxtSeoModules(nuxt?: Nuxt): NuxtSeoModuleDetection[];
declare function useModuleLogger(name: string, options: {
    debug?: boolean;
}, nuxt?: Nuxt): ReturnType<typeof useLogger>;
declare function detectTarget(options?: {
    static?: boolean;
}): string | undefined;
declare function resolveNitroPreset(nitroConfig?: NitroConfig): string;
/**
 * Get the user provided options for a Nuxt module.
 *
 * These options may not be the resolved options that the module actually uses.
 */
declare function getNuxtModuleOptions(module: string | NuxtModule, nuxt?: Nuxt): Promise<Record<string, any>>;
declare function isNuxtGenerate(nuxt?: Nuxt): boolean;
/**
 * Generate TypeScript type augmentations for a Nuxt module.
 */
declare function extendTypes(module: string, template: (options: {
    typesPath: string;
}) => string | Promise<string>): void;
/**
 * Create a promise that resolves when Nuxt pages are resolved.
 */
declare function createPagesPromise(nuxt?: Nuxt): Promise<NuxtPage[]>;
/**
 * Create a promise that resolves when Nitro is initialized.
 */
declare function createNitroPromise(nuxt?: Nuxt): Promise<Nitro>;
interface NuxtContentVersion {
    version: 2 | 3;
}
/**
 * Detect which version of @nuxt/content is installed.
 *
 * Returns `false` when @nuxt/content is not installed or the version is unrecognised.
 */
declare function resolveNuxtContentVersion(): Promise<false | NuxtContentVersion>;
/**
 * Read the major version of a non-module package as resolved from `rootDir`.
 *
 * Unlike `hasNuxtModuleCompatibility`, this works for plain libraries (e.g.
 * `unhead`, `@unhead/vue`) that aren't registered as Nuxt modules. Returns
 * `undefined` when the package can't be resolved or has no parseable version.
 */
declare function resolvePackageMajor(id: string, rootDir: string): Promise<number | undefined>;
type UnheadMajor = 2 | 3;
/**
 * Resolve the major of the unhead the host app renders with.
 *
 * `@unhead/vue` is what the head-stack packages peer-depend on, so it's the
 * primary signal; falls back to the core `unhead` package, then to `3` (the
 * current default major) when neither resolves.
 *
 * Used to keep head-stack dependencies on a compatible major. For example,
 * `@unhead/schema-org` v3 attaches an object `_resolver` to every graph node
 * that unhead v2's `walkResolver` invokes as a thunk, crashing render; a module
 * that ships both majors can use this to alias to the matching one.
 */
declare function resolveHostUnheadMajor(rootDir: string): Promise<UnheadMajor>;
declare const COMARK_CONTENT_MODULE = "@harlan-zw/comark-content";
/**
 * The Markdown content module backing this app, if any.
 *
 * `@nuxt/content` and `comark-content` both fire the `content:file:beforeParse`
 * and `content:file:afterParse` build hooks with the same context shape, so a
 * module's frontmatter handling is written once. They differ at runtime:
 * `@nuxt/content` queries a SQL database, comark reads Nitro server assets.
 */
type ContentProvider = {
    _tag: 'None';
} | {
    _tag: 'NuxtContent';
    version: 2 | 3;
} | {
    _tag: 'Comark';
};
/**
 * Detect which Markdown content module is installed.
 *
 * `@nuxt/content` wins when both are present: it owns the `content` config key
 * and its runtime is the one the app's pages query.
 */
declare function resolveContentProvider(nuxt?: Nuxt): Promise<ContentProvider>;
/**
 * Whether the provider fires the `content:file:*` build hooks, which is where
 * every module maps its frontmatter field onto the parsed page.
 */
declare function hasContentFileHooks(provider: ContentProvider): boolean;
/**
 * Alias `#nuxtseo/content` to the shim for the detected provider.
 *
 * Consumers import collection enumeration and page queries from that one
 * specifier instead of naming `@nuxt/content/server` or
 * `@harlan-zw/comark-content/server`. Naming a package directly would put it in
 * every build, and a build without that package installed fails to bundle.
 *
 * Nuxt Content v2 has no collection model, so it resolves to the empty shim.
 * A module that supports v2 keeps its own v2 path.
 */
declare function setupContentRuntime(provider: ContentProvider, nuxt?: Nuxt): void;

export { COMARK_CONTENT_MODULE, createNitroPromise, createPagesPromise, detectNuxtSeoModules, detectTarget, extendTypes, getNuxtModuleOptions, hasContentFileHooks, isNuxtGenerate, renderNitroTypeAugmentations, resolveContentProvider, resolveHostUnheadMajor, resolveNitroPreset, resolveNuxtContentVersion, resolvePackageMajor, setupContentRuntime, setupNitroRuntimeCompatibility, useModuleLogger };
export type { ContentProvider, NitroRuntimeCompatibility, NitroTypeAugmentations, NuxtContentVersion, NuxtSeoModuleDetection, UnheadMajor };
