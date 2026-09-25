export function buildSchemaOrgContentScript(schemaOrgInput, defineWebPage, scriptAttributes) {
  const nodes = Array.isArray(schemaOrgInput) ? schemaOrgInput : [defineWebPage(schemaOrgInput)];
  const replaceType = (node) => {
    if (node.type) {
      node["@type"] = node.type;
      delete node.type;
    }
    Object.entries(node).forEach(([, value]) => {
      if (typeof value === "object") {
        replaceType(value);
      }
    });
    return node;
  };
  return {
    type: "application/ld+json",
    key: "schema-org-graph",
    nodes: nodes.map(replaceType),
    ...scriptAttributes || {}
  };
}
