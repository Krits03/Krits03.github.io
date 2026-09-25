import { createContentSchemaFactory } from 'nuxtseo-shared/content';
import { z } from 'zod';

const { defineSchema: defineSchemaOrgSchema, schema } = createContentSchemaFactory({
  fieldName: "schemaOrg",
  label: "schema-org",
  docsUrl: "https://nuxtseo.com/schema-org/guides/content",
  buildSchema: (_z) => {
    const node = _z.record(_z.string(), _z.any());
    return _z.union([node, _z.array(node).optional()]).optional();
  }
}, z);
const schemaOrgSchema = schema.shape.schemaOrg;
const headSchema = z.object({
  head: z.object({
    meta: z.array(z.record(z.string(), z.any()).optional()),
    script: z.array(z.record(z.string(), z.any()).optional())
  }).optional()
});
function asSchemaOrgCollection(collection) {
  console.warn("[schema-org] `asSchemaOrgCollection()` is deprecated. Use `defineSchemaOrgSchema()` in your collection schema instead. See https://nuxtseo.com/schema-org/guides/content");
  if (collection.type === "page") {
    collection.schema = collection.schema ? schema.extend(collection.schema.shape) : schema;
    if (!("head" in collection.schema.shape)) {
      collection.schema = headSchema.extend(collection.schema.shape);
    }
  }
  return collection;
}

export { asSchemaOrgCollection, defineSchemaOrgSchema, schema, schemaOrgSchema };
