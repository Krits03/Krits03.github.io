import { d as defineSchemaOrgResolver, a9 as IdentityId, aa as resolveDefaultType, e as resolveRelation, a as resolveNode } from '../shared/schema-org.BygE6hLl.mjs';
import { openingHoursResolver } from './index24.mjs';
import { o as organizationResolver } from './index3.mjs';
import { addressResolver } from './index28.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import './index16.mjs';
import './index40.mjs';
import './index39.mjs';

const localBusinessResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": ["Organization", "LocalBusiness"]
  },
  inheritMeta: [
    { key: "url", meta: "host" },
    { key: "currenciesAccepted", meta: "currency" }
  ],
  idPrefix: ["host", IdentityId],
  resolve(node, ctx) {
    resolveDefaultType(node, ["Organization", "LocalBusiness"]);
    node.address = resolveRelation(node.address, ctx, addressResolver);
    node.openingHoursSpecification = resolveRelation(node.openingHoursSpecification, ctx, openingHoursResolver);
    node = resolveNode({ ...node }, ctx, organizationResolver);
    return node;
  },
  resolveRootNode(node, ctx) {
    organizationResolver.resolveRootNode(node, ctx);
    return node;
  }
});

export { localBusinessResolver };
