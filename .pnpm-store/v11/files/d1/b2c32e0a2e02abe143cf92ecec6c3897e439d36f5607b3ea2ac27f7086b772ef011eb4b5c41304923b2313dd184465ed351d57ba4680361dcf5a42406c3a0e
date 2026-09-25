import { d as defineSchemaOrgResolver, e as resolveRelation, a6 as setIfEmpty } from '../shared/schema-org.BygE6hLl.mjs';
import { listItemResolver } from './index16.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';

const itemListResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "ItemList"
  },
  resolve(node, ctx) {
    if (node.itemListElement) {
      let index = 1;
      node.itemListElement = resolveRelation(node.itemListElement, ctx, listItemResolver, {
        array: true,
        afterResolve(node2) {
          setIfEmpty(node2, "position", index++);
        }
      });
    }
    return node;
  }
});

export { itemListResolver };
