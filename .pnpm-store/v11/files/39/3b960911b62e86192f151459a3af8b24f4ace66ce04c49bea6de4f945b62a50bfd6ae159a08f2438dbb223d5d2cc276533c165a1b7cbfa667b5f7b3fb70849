import type { DefineComponent } from 'vue';
import type { DirectImportInfo } from './schema.js';
export declare function useLazyComponentTracking(components?: DirectImportInfo[]): any;
/**
 * Wrap components definition like with defineComponent or defineNuxtComponent or just sfc exports
 */
export declare function __wrapMainComponent(component: DefineComponent, imports?: DirectImportInfo[]): DefineComponent;
/**
 * Wrap imported components to track their usage.
 */
export declare function __wrapImportedComponent(component: DefineComponent, componentName: string, importSource: string, importedBy: string): DefineComponent;
