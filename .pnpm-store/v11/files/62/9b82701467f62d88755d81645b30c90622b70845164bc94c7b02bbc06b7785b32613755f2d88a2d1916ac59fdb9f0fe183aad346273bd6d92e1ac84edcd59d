import { Resolver } from '@nuxt/kit';
import { BirpcGroup } from 'birpc';
export { BirpcGroup } from 'birpc';
import { Nuxt } from 'nuxt/schema';

/** Origin-root route the assembled (layer-mode) devtools client is served from. */
declare const UNIFIED_CLIENT_ROUTE = "/__nuxt-seo-devtools";
interface DevToolsUIConfig {
    /** Per-module route used by the legacy prebuilt-client mode. */
    route?: string;
    name: string;
    title: string;
    icon: string;
    /** Route segment inside the unified client (layer mode). Defaults to name minus `nuxt-`. */
    slug?: string;
    /** Legacy dev-proxy port (prebuilt-client mode only). */
    devPort?: number;
}
interface SeoModuleInfo {
    name: string;
    /** npm package name — the stable identifier the client matches installed state on. */
    npm?: string;
    title: string;
    icon: string;
    route: string;
}
/**
 * Register a module's devtools panel. Detects whether the module ships a source layer
 * (current) or a prebuilt client (legacy) and handles each, so old and new modules can
 * be mixed during migration.
 */
declare function setupDevToolsUI(config: DevToolsUIConfig, resolve: Resolver['resolve'], nuxt?: Nuxt): void;
declare function setupDevToolsRpc<ServerFunctions extends object, ClientFunctions extends object>(namespace: string, serverFunctions: ServerFunctions, nuxt?: Nuxt): Promise<BirpcGroup<ClientFunctions, ServerFunctions>>;

export { UNIFIED_CLIENT_ROUTE, setupDevToolsRpc, setupDevToolsUI };
export type { DevToolsUIConfig, SeoModuleInfo };
