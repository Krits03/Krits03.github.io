import * as nuxtseo_shared_content from 'nuxtseo-shared/content';
import { Collection } from '@nuxt/content';
import { z } from 'zod';

declare const defineSchemaOrgSchema: (options?: nuxtseo_shared_content.ContentSchemaOptions) => z.ZodOptional<z.ZodUnion<readonly [z.ZodRecord<z.ZodString, z.ZodAny>, z.ZodOptional<z.ZodArray<z.ZodRecord<z.ZodString, z.ZodAny>>>]>>;
declare const schema: z.ZodObject<{
    [x: string]: any;
}, z.core.$strip>;

declare const schemaOrgSchema: any;
/** @deprecated Use `defineSchemaOrgSchema()` in your collection schema instead. See https://nuxtseo.com/schema-org/guides/content */
declare function asSchemaOrgCollection<T>(collection: Collection<T>): Collection<T>;

export { asSchemaOrgCollection, defineSchemaOrgSchema, schema, schemaOrgSchema };
