import { createContentSchemaFactory } from 'nuxtseo-shared/content';
import { z } from 'zod';

const { defineSchema, asCollection, schema } = createContentSchemaFactory({
  fieldName: "robots",
  label: "robots",
  docsUrl: "https://nuxtseo.com/robots/guides/content",
  buildSchema: (_z) => _z.union([_z.string(), _z.boolean()]).optional()
}, z);
function asRobotsCollection(collection) {
  return asCollection(collection);
}

export { asRobotsCollection, defineSchema as defineRobotsSchema, schema };
