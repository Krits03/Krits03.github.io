import * as nuxtseo_shared_content from 'nuxtseo-shared/content';
import { z } from 'zod';

declare const defineSchema: (options?: nuxtseo_shared_content.ContentSchemaOptions | undefined) => z.ZodOptional<z.ZodObject<{
    url: z.ZodOptional<z.ZodString>;
    component: z.ZodOptional<z.ZodString>;
    props: z.ZodRecord<z.ZodString, z.ZodAny>;
}, z.core.$strip>>;
declare const asCollection: <T>(collection: any) => T;
declare const schema: z.ZodObject<{
    [x: string]: any;
}, z.core.$strip>;

declare const ogImageSchema: any;

export { asCollection as asOgImageCollection, defineSchema as defineOgImageSchema, ogImageSchema, schema };
