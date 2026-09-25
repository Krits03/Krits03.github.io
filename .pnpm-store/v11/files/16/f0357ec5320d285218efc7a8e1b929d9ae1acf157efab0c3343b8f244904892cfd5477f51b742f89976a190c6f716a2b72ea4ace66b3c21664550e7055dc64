import * as contentRuntime from "#nuxtseo/content";
import { defineEventHandler } from "#nuxtseo/h3";
import { filters } from "#sitemap/content-filters";
import { onUrlFns } from "#sitemap/content-on-url";
const { listPageCollections, provider, queryPages } = contentRuntime;
export default defineEventHandler(async (e) => {
  const collections = (await listPageCollections(e)).filter((collection) => collection.inSitemap && collection.hasField("sitemap")).map((collection) => collection.name);
  const results = await Promise.all(collections.map(async (collection) => {
    const needsAllFields = filters?.has(collection) || onUrlFns?.has(collection);
    const query = queryPages(e, collection).where("path", "IS NOT NULL").where("sitemap", "IS NOT NULL");
    if (!needsAllFields)
      query.select("path", "sitemap");
    try {
      const entries = await query.all();
      const filter = filters?.get(collection);
      return { collection, entries: filter ? entries.filter(filter) : entries };
    } catch (err) {
      const hint = provider === "nuxt-content-v3" ? " On serverless the content DB is restored from a prerendered sql_dump.txt that isn't readable inside the function (nuxt/content#3805). Fix: prerender the sitemap so content URLs resolve at build, or configure a runtime database (D1/Turso/Postgres)." : "";
      console.error(`[@nuxtjs/sitemap] Couldn't query content collection "${collection}" for the sitemap, so its URLs will be missing.${hint}`, err);
      return { collection, entries: [] };
    }
  }));
  return results.flatMap(({ collection, entries }) => {
    const onUrl = onUrlFns?.get(collection);
    return entries.filter((entry) => entry.sitemap !== false && entry.path && !entry.path.endsWith(".navigation")).map((entry) => {
      const url = {
        loc: entry.path,
        ...typeof entry.sitemap === "object" && entry.sitemap ? entry.sitemap : {}
      };
      onUrl?.(url, entry, collection);
      return url;
    });
  });
});
