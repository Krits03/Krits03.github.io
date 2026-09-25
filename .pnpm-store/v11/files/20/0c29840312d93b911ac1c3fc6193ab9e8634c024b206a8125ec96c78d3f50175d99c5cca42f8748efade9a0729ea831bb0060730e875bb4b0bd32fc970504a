import { PageCollectionItemBase, Collection } from '@nuxt/content';
import { z, TypeOf } from 'zod';

declare global {
    var __sitemapCollectionFilters: Map<string, (entry: any) => boolean> | undefined;
    var __sitemapCollectionOnUrlFns: Map<string, (url: any, entry: any, collection: string) => void> | undefined;
}
interface DefineSitemapSchemaOptions<TEntry = Record<string, unknown>> {
    z?: typeof z;
    name?: string;
    filter?: (entry: PageCollectionItemBase & SitemapSchema & TEntry) => boolean;
    onUrl?: (url: {
        loc: string;
        lastmod?: string | Date;
        changefreq?: string;
        priority?: number;
        images?: {
            loc: string;
        }[];
        videos?: {
            content_loc: string;
        }[];
        [key: string]: unknown;
    }, entry: PageCollectionItemBase & SitemapSchema & TEntry, collection: string) => void;
}
declare const defineSchema: (options?: DefineSitemapSchemaOptions<Record<string, unknown>> | undefined) => z.ZodOptional<z.ZodObject<{
    loc: z.ZodOptional<z.ZodString>;
    lastmod: z.ZodOptional<z.ZodDate>;
    changefreq: z.ZodOptional<z.ZodUnion<readonly [z.ZodLiteral<"always">, z.ZodLiteral<"hourly">, z.ZodLiteral<"daily">, z.ZodLiteral<"weekly">, z.ZodLiteral<"monthly">, z.ZodLiteral<"yearly">, z.ZodLiteral<"never">]>>;
    priority: z.ZodOptional<z.ZodNumber>;
    images: z.ZodOptional<z.ZodArray<z.ZodObject<{
        loc: z.ZodString;
        caption: z.ZodOptional<z.ZodString>;
        geo_location: z.ZodOptional<z.ZodString>;
        title: z.ZodOptional<z.ZodString>;
        license: z.ZodOptional<z.ZodString>;
    }, z.core.$strip>>>;
    videos: z.ZodOptional<z.ZodArray<z.ZodObject<{
        content_loc: z.ZodString;
        player_loc: z.ZodOptional<z.ZodString>;
        duration: z.ZodOptional<z.ZodString>;
        expiration_date: z.ZodOptional<z.ZodDate>;
        rating: z.ZodOptional<z.ZodNumber>;
        view_count: z.ZodOptional<z.ZodNumber>;
        publication_date: z.ZodOptional<z.ZodDate>;
        family_friendly: z.ZodOptional<z.ZodBoolean>;
        tag: z.ZodOptional<z.ZodString>;
        category: z.ZodOptional<z.ZodString>;
        restriction: z.ZodOptional<z.ZodObject<{
            relationship: z.ZodOptional<z.ZodLiteral<"allow">>;
            value: z.ZodOptional<z.ZodString>;
        }, z.core.$strip>>;
        gallery_loc: z.ZodOptional<z.ZodString>;
        price: z.ZodOptional<z.ZodString>;
        requires_subscription: z.ZodOptional<z.ZodBoolean>;
        uploader: z.ZodOptional<z.ZodString>;
    }, z.core.$strip>>>;
}, z.core.$strip>>;
declare const schema: z.ZodObject<{
    [x: string]: any;
}, z.core.$strip>;

type SitemapSchema = TypeOf<typeof schema>;
/** @deprecated Use `defineSitemapSchema()` in your collection schema instead. See https://nuxtseo.com/sitemap/guides/content */
declare function asSitemapCollection<T>(collection: Collection<T>, options?: DefineSitemapSchemaOptions<T>): Collection<T>;

export { asSitemapCollection, defineSchema as defineSitemapSchema, schema };
export type { DefineSitemapSchemaOptions, SitemapSchema };
