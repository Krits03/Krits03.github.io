import { d as defineSchemaOrgResolver, e as resolveRelation, a6 as setIfEmpty, ac as asArray } from '../shared/schema-org.BygE6hLl.mjs';
import { offerResolver } from './index23.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import '../shared/schema-org.Ba1paCCL.mjs';

const aggregateOfferResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "AggregateOffer"
  },
  inheritMeta: [
    { meta: "currency", key: "priceCurrency" }
  ],
  resolve(node, ctx) {
    node.offers = resolveRelation(node.offers, ctx, offerResolver);
    if (node.offers)
      setIfEmpty(node, "offerCount", asArray(node.offers).length);
    return node;
  }
});

export { aggregateOfferResolver };
