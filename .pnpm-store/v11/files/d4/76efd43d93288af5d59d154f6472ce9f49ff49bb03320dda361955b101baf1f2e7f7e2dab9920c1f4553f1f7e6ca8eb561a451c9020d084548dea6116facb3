import { z } from 'zod';

type Zod = typeof z;
interface ContentSchemaOptions {
    /**
     * Pass the `z` instance from `@nuxt/content` to ensure `.editor()` works
     * across Zod versions. When omitted, the module's bundled `z` is used.
     */
    z?: Zod;
}
interface ContentEditorConfig {
    hidden?: boolean;
    input?: 'media' | 'icon' | 'textarea';
    iconLibraries?: string[];
}
/**
 * Apply Nuxt Content `.editor()` metadata to a zod schema field.
 * No-ops gracefully when `.editor()` is not patched onto ZodType (outside Nuxt Content).
 */
declare function withEditor<T>(schema: T, config: ContentEditorConfig): T;
/**
 * Hide a zod schema field from the Nuxt Content / Studio editor.
 */
declare function withEditorHidden<T>(schema: T): T;
interface DefineContentSchemaConfig<TSchema = any, TDefineOptions extends ContentSchemaOptions = ContentSchemaOptions> {
    /**
     * The field name used in frontmatter (e.g. 'robots', 'sitemap', 'ogImage').
     */
    fieldName: string;
    /**
     * Build the zod schema for this field. Receives the zod instance
     * (either the user's `@nuxt/content` patched version or the module's bundled one).
     */
    buildSchema: (z: Zod) => TSchema;
    /**
     * Module label for deprecation warnings (e.g. 'robots', 'sitemap').
     */
    label: string;
    /**
     * Documentation URL for migration guidance.
     */
    docsUrl?: string;
    /**
     * Hook called when `defineSchema()` is invoked. Use for validation or
     * registering module-specific side effects (e.g. sitemap filter/onUrl).
     */
    onDefineSchema?: (options: TDefineOptions) => void;
}
/**
 * Factory for creating a module's `define*Schema()` and deprecated `as*Collection()` exports.
 *
 * Each module provides its own schema builder. The factory handles:
 * - Zod instance passthrough for `@nuxt/content` version compatibility
 * - Consistent `DefineSchemaOptions` interface
 * - Deprecated `asXxxCollection()` wrapper with migration warning
 *
 * @example
 * import { z } from 'zod'
 * import { createContentSchemaFactory } from 'nuxtseo-shared/content'
 *
 * const { defineSchema, asCollection, schema } = createContentSchemaFactory({
 *   fieldName: 'robots',
 *   label: 'robots',
 *   docsUrl: 'https://nuxtseo.com/robots/guides/content',
 *   buildSchema: (z) => z.union([z.string(), z.boolean()]).optional(),
 * }, z)
 *
 * export { defineSchema as defineRobotsSchema, asCollection as asRobotsCollection, schema }
 */
declare function createContentSchemaFactory<TSchema, TDefineOptions extends ContentSchemaOptions = ContentSchemaOptions>(config: DefineContentSchemaConfig<TSchema, TDefineOptions>, defaultZ: Zod): {
    defineSchema: (options?: TDefineOptions) => TSchema;
    asCollection: <T>(collection: any) => T;
    schema: z.ZodObject<{
        [x: string]: any;
    }, z.core.$strip>;
    fieldSchema: TSchema;
};

export { createContentSchemaFactory, withEditor, withEditorHidden };
export type { ContentEditorConfig, ContentSchemaOptions, DefineContentSchemaConfig, Zod };
