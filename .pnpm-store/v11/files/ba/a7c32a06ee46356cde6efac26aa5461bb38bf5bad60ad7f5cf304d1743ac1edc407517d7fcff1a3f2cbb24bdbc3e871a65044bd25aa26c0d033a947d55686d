import { d as defineSchemaOrgResolver, a9 as IdentityId, aa as resolveDefaultType, e as resolveRelation, a as resolveNode } from '../shared/schema-org.BygE6hLl.mjs';
import { localBusinessResolver } from './index17.mjs';
import { r as ratingResolver } from '../shared/schema-org.SD01-lvP.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import './index24.mjs';
import './index3.mjs';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';

const foodEstablishmentResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": ["Organization", "LocalBusiness", "FoodEstablishment"]
  },
  inheritMeta: [
    { key: "url", meta: "host" },
    { key: "currenciesAccepted", meta: "currency" }
  ],
  idPrefix: ["host", IdentityId],
  resolve(node, ctx) {
    resolveDefaultType(node, ["Organization", "LocalBusiness", "FoodEstablishment"]);
    node.starRating = resolveRelation(node.starRating, ctx, ratingResolver);
    node = resolveNode(node, ctx, localBusinessResolver);
    return node;
  },
  resolveRootNode(node, ctx) {
    localBusinessResolver.resolveRootNode(node, ctx);
    return node;
  }
});

export { foodEstablishmentResolver };
