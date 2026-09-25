import { d as defineSchemaOrgResolver } from '../shared/schema-org.BygE6hLl.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';

const readActionResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "ReadAction"
  },
  resolve(node, ctx) {
    if (!node.target.includes(ctx.meta.url))
      node.target.unshift(ctx.meta.url);
    return node;
  }
});

export { readActionResolver };
