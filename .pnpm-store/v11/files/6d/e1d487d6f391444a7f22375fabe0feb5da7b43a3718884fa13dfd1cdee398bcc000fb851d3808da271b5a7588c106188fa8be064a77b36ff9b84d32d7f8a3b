import { createContentSchemaFactory } from 'nuxtseo-shared/content';
import { z } from 'zod';

if (!globalThis.__sitemapCollectionFilters)
  globalThis.__sitemapCollectionFilters = /* @__PURE__ */ new Map();
if (!globalThis.__sitemapCollectionOnUrlFns)
  globalThis.__sitemapCollectionOnUrlFns = /* @__PURE__ */ new Map();
const collectionFilters = globalThis.__sitemapCollectionFilters;
const collectionOnUrlFns = globalThis.__sitemapCollectionOnUrlFns;
function registerCollectionHooks(options, callerName) {
  if (!options?.filter && !options?.onUrl)
    return;
  if (!options.name)
    throw new Error(`[sitemap] \`name\` is required when using \`filter\` or \`onUrl\` in ${callerName}()`);
  if (options.filter)
    collectionFilters.set(options.name, options.filter);
  if (options.onUrl)
    collectionOnUrlFns.set(options.name, options.onUrl);
}
const { defineSchema, asCollection, schema } = createContentSchemaFactory({
  fieldName: "sitemap",
  label: "sitemap",
  docsUrl: "https://nuxtseo.com/sitemap/guides/content",
  buildSchema: (_z) => buildSitemapObjectSchema(_z),
  onDefineSchema: (options) => {
    if ("type" in options || "source" in options)
      throw new Error("[sitemap] `defineSitemapSchema()` returns a schema field, not a collection wrapper. Use it inside your schema: `schema: z.object({ sitemap: defineSitemapSchema() })`. See https://nuxtseo.com/sitemap/guides/content");
    warnIfZodMismatch(options?.z);
    registerCollectionHooks(options, "defineSitemapSchema");
  }
}, z);
function asSitemapCollection(collection, options) {
  if (options?.filter || options?.onUrl) {
    if (!options.name)
      throw new Error("[sitemap] `name` is required when using `filter` or `onUrl` in asSitemapCollection()");
    if (options.filter)
      collectionFilters.set(options.name, options.filter);
    if (options.onUrl)
      collectionOnUrlFns.set(options.name, options.onUrl);
  }
  try {
    return asCollection(collection);
  } catch (e) {
    console.warn(
      `[sitemap] Failed to apply sitemap schema to collection. This is likely a Zod version mismatch.`,
      `Pass your Zod instance explicitly: \`defineSitemapSchema({ z })\`. See https://nuxtseo.com/sitemap/guides/content`,
      `Error: ${e.message}`
    );
    return collection;
  }
}
let _hasWarnedZodMismatch = false;
function warnIfZodMismatch(userZ) {
  if (_hasWarnedZodMismatch || userZ)
    return;
  const testSchema = z.object({});
  const hasV3 = "_def" in testSchema && !("def" in testSchema);
  const hasV4 = "def" in testSchema;
  if (hasV3 || hasV4) {
    if (hasV3) {
      _hasWarnedZodMismatch = true;
      console.warn(
        `[sitemap] Zod 3 detected but @nuxt/content v3 expects Zod 4.`,
        `Pass your zod instance explicitly: \`defineSitemapSchema({ z })\`.`,
        `See https://nuxtseo.com/sitemap/guides/content`
      );
    }
  }
}
function buildSitemapObjectSchema(_z) {
  return _z.object({
    loc: _z.string().optional(),
    lastmod: _z.date().optional(),
    changefreq: _z.union([_z.literal("always"), _z.literal("hourly"), _z.literal("daily"), _z.literal("weekly"), _z.literal("monthly"), _z.literal("yearly"), _z.literal("never")]).optional(),
    priority: _z.number().optional(),
    images: _z.array(_z.object({
      loc: _z.string(),
      caption: _z.string().optional(),
      geo_location: _z.string().optional(),
      title: _z.string().optional(),
      license: _z.string().optional()
    })).optional(),
    videos: _z.array(_z.object({
      content_loc: _z.string(),
      player_loc: _z.string().optional(),
      duration: _z.string().optional(),
      expiration_date: _z.date().optional(),
      rating: _z.number().optional(),
      view_count: _z.number().optional(),
      publication_date: _z.date().optional(),
      family_friendly: _z.boolean().optional(),
      tag: _z.string().optional(),
      category: _z.string().optional(),
      restriction: _z.object({
        relationship: _z.literal("allow").optional(),
        value: _z.string().optional()
      }).optional(),
      gallery_loc: _z.string().optional(),
      price: _z.string().optional(),
      requires_subscription: _z.boolean().optional(),
      uploader: _z.string().optional()
    })).optional()
  }).optional();
}

export { asSitemapCollection, defineSchema as defineSitemapSchema, schema };
