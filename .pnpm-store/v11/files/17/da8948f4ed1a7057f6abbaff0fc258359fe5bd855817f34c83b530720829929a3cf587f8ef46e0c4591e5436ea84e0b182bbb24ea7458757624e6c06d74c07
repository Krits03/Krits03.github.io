import * as _nuxt_schema from '@nuxt/schema';
import { NuxtSeoModuleDetection } from './kit.js';
import 'nitropack';
import 'nitropack/types';
import 'nuxt/schema';
import '@nuxt/kit';

interface ModuleHooks {
    'nuxt-seo-pro:modules': (modules: NuxtSeoModuleDetection[]) => Promise<void> | void;
}
declare module '@nuxt/schema' {
    interface NuxtHooks extends ModuleHooks {
    }
}
declare const _default: _nuxt_schema.NuxtModule<_nuxt_schema.ModuleOptions, _nuxt_schema.ModuleOptions, false>;

export { _default as default };
export type { ModuleHooks };
