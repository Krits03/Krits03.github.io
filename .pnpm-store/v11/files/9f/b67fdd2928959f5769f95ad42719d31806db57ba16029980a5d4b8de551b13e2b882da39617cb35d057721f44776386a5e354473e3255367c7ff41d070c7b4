'use strict';

const content = require('nuxtseo-shared/content');
const zod = require('zod');

const { defineSchema: defineSchemaOrgSchema, schema } = content.createContentSchemaFactory({
  fieldName: "schemaOrg",
  label: "schema-org",
  docsUrl: "https://nuxtseo.com/schema-org/guides/content",
  buildSchema: (_z) => {
    const node = _z.record(_z.string(), _z.any());
    return _z.union([node, _z.array(node).optional()]).optional();
  }
}, zod.z);
const schemaOrgSchema = schema.shape.schemaOrg;
const headSchema = zod.z.object({
  head: zod.z.object({
    meta: zod.z.array(zod.z.record(zod.z.string(), zod.z.any()).optional()),
    script: zod.z.array(zod.z.record(zod.z.string(), zod.z.any()).optional())
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

exports.asSchemaOrgCollection = asSchemaOrgCollection;
exports.defineSchemaOrgSchema = defineSchemaOrgSchema;
exports.schema = schema;
exports.schemaOrgSchema = schemaOrgSchema;
