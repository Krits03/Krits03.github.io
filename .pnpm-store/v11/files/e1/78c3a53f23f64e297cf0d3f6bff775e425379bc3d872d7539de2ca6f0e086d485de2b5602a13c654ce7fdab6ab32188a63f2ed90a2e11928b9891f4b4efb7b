import { queryCollection, queryCollectionManifest } from "@harlan-zw/comark-content/server";
export const provider = "comark";
export async function listPageCollections(event) {
  const manifest = await queryCollectionManifest(event);
  return manifest.map((entry) => ({
    name: entry.name,
    // comark derives no field list from a schema, so every field is available to ask
    // for. A collection opts out of the sitemap on the collection itself.
    hasField: () => true,
    inSitemap: entry.sitemap
  }));
}
export function queryPages(event, collection) {
  const wheres = [];
  let selected;
  const query = {
    where(field, operator, value) {
      wheres.push([field, operator, value]);
      return query;
    },
    select(...fields) {
      selected = fields;
      return query;
    },
    async all() {
      const notNull = wheres.filter(([, operator]) => operator === "IS NOT NULL").map(([field]) => field);
      const builder = queryCollection(event, collection);
      for (const [field, operator, value] of wheres) {
        if (operator !== "IS NOT NULL")
          builder.where(field, operator, value);
      }
      if (selected)
        builder.select(.../* @__PURE__ */ new Set([...selected, ...notNull]));
      const rows = await builder.all();
      return rows.filter((row) => notNull.every((field) => row[field] !== null && row[field] !== void 0));
    },
    async first() {
      return (await query.all())[0] ?? null;
    }
  };
  return query;
}
