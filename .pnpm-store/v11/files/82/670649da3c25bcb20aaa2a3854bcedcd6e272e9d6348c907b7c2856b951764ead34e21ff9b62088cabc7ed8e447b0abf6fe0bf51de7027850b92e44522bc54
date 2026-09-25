import { d as defineSchemaOrgResolver, ad as resolveWithBase, e as resolveRelation } from '../shared/schema-org.BygE6hLl.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';

const listItemResolver = defineSchemaOrgResolver({
  cast(node) {
    if (typeof node === "string") {
      node = {
        name: node
      };
    }
    return node;
  },
  defaults: {
    "@type": "ListItem"
  },
  resolve(node, ctx) {
    if (typeof node.item === "string")
      node.item = resolveWithBase(ctx.meta.host, node.item);
    else if (typeof node.item === "object")
      node.item = resolveRelation(node.item, ctx);
    return node;
  }
});

export { listItemResolver };
