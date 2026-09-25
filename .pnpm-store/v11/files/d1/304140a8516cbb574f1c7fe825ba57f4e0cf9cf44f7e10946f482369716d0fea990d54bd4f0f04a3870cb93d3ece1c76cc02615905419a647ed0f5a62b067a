import { d as defineSchemaOrgResolver } from '../shared/schema-org.BygE6hLl.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';

const virtualLocationResolver = defineSchemaOrgResolver({
  cast(node) {
    if (typeof node === "string") {
      return {
        url: node
      };
    }
    return node;
  },
  defaults: {
    "@type": "VirtualLocation"
  }
});

export { virtualLocationResolver };
