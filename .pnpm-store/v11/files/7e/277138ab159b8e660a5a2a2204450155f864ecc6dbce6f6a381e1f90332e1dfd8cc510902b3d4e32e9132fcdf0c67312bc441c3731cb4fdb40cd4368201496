import type { NuxtModule } from '@nuxt/schema'

import type { default as Module, ModuleHooks } from './module.mjs'

declare module '@nuxt/schema' {
  interface NuxtHooks extends ModuleHooks {}
}

export type ModuleOptions = typeof Module extends NuxtModule<infer O> ? Partial<O> : Record<string, any>

export { default } from './module.mjs'

export { type ModuleHooks } from './module.mjs'
