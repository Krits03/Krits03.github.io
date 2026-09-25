import { d as defineSchemaOrgResolver, ad as resolveWithBase } from '../shared/schema-org.BygE6hLl.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';

const searchActionResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "SearchAction",
    "target": {
      "@type": "EntryPoint"
    },
    "query-input": {
      "@type": "PropertyValueSpecification",
      "valueRequired": true,
      "valueName": "search_term_string"
    }
  },
  resolve(node, ctx) {
    if (typeof node.target === "string") {
      node.target = {
        "@type": "EntryPoint",
        "urlTemplate": resolveWithBase(ctx.meta.host, node.target)
      };
    }
    return node;
  }
});

export { searchActionResolver };
