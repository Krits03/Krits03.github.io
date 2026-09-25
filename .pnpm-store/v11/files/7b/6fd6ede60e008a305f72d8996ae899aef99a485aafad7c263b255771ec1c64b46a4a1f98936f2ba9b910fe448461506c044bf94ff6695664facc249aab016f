'use strict';

const content = require('nuxtseo-shared/content');
const zod = require('zod');

const { defineSchema, asCollection, schema } = content.createContentSchemaFactory({
  fieldName: "robots",
  label: "robots",
  docsUrl: "https://nuxtseo.com/robots/guides/content",
  buildSchema: (_z) => _z.union([_z.string(), _z.boolean()]).optional()
}, zod.z);
function asRobotsCollection(collection) {
  return asCollection(collection);
}

exports.asRobotsCollection = asRobotsCollection;
exports.defineRobotsSchema = defineSchema;
exports.schema = schema;
