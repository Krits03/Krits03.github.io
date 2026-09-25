import * as nuxtseo_shared_content from 'nuxtseo-shared/content';
import { Collection } from '@nuxt/content';
import { z } from 'zod';

declare const defineSchema: (options?: nuxtseo_shared_content.ContentSchemaOptions | undefined) => z.ZodOptional<z.ZodUnion<[z.ZodString, z.ZodBoolean]>>;
declare const schema: z.ZodObject<{
    [x: string]: any;
}, z.core.$strip, z.ZodTypeAny, {
    [x: string]: any;
}, {
    [x: string]: any;
}>;

/** @deprecated Use `defineRobotsSchema()` in your collection schema instead. See https://nuxtseo.com/robots/advanced/content */
declare function asRobotsCollection<T>(collection: Collection<T>): Collection<T>;

export { asRobotsCollection, defineSchema as defineRobotsSchema, schema };
