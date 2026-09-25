function withEditor(schema, config) {
  if (typeof schema.editor === "function")
    return schema.editor(config);
  return schema;
}
function withEditorHidden(schema) {
  return withEditor(schema, { hidden: true });
}
function createContentSchemaFactory(config, defaultZ) {
  const { fieldName, buildSchema, label, docsUrl, onDefineSchema } = config;
  const schemaObject = defaultZ.object({ [fieldName]: buildSchema(defaultZ) });
  function defineSchema(options) {
    if (options && onDefineSchema)
      onDefineSchema(options);
    const _z = options?.z ?? defaultZ;
    return buildSchema(_z);
  }
  function asCollection(collection) {
    const migrationHint = docsUrl ? ` See ${docsUrl}` : "";
    console.warn(`[${label}] \`as${capitalize(label)}Collection()\` is deprecated. Use \`define${capitalize(label)}Schema()\` in your collection schema instead.${migrationHint}`);
    if (collection.type === "page") {
      try {
        collection.schema = collection.schema ? schemaObject.extend(collection.schema.shape) : schemaObject;
      } catch (e) {
        console.warn(
          `[${label}] Failed to apply ${label} schema to collection. This is likely a Zod version mismatch.`,
          `Pass your Zod instance explicitly: \`define${capitalize(label)}Schema({ z })\`.${migrationHint}`,
          `Error: ${e.message}`
        );
      }
    }
    return collection;
  }
  return {
    defineSchema,
    asCollection,
    schema: schemaObject,
    fieldSchema: buildSchema(defaultZ)
  };
}
function capitalize(s) {
  return s.charAt(0).toUpperCase() + s.slice(1);
}

export { createContentSchemaFactory, withEditor, withEditorHidden };
