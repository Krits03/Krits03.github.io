import { queryCollection } from "@nuxt/content/server";
import manifest from "#content/manifest";
export const provider = "nuxt-content-v3";
export async function listPageCollections(_event) {
  return Object.entries(manifest).map(([name, entry]) => ({
    name,
    hasField: (field) => !!entry.fields && field in entry.fields,
    // @nuxt/content has no collection level sitemap opt out. The schema field is
    // the opt in, which `hasField` answers.
    inSitemap: true
  }));
}
export function queryPages(event, collection) {
  return queryCollection(event, collection);
}
