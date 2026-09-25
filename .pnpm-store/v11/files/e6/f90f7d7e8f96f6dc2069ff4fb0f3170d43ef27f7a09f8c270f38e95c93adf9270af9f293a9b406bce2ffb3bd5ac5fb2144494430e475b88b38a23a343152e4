import { d as defineSchemaOrgResolver, a9 as IdentityId, a6 as setIfEmpty, a7 as idReference, aa as resolveDefaultType, e as resolveRelation } from '../shared/schema-org.BygE6hLl.mjs';
import { aggregateRatingResolver } from './index2.mjs';
import { offerResolver } from './index23.mjs';
import { reviewResolver } from './index32.mjs';
import { d as PrimaryWebPageId } from './index3.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import '../shared/schema-org.Ba1paCCL.mjs';
import '../shared/schema-org.SD01-lvP.mjs';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';

const ServiceId = "#service";
const serviceResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "Service"
  },
  inheritMeta: [
    "description",
    "image",
    { meta: "title", key: "name" }
  ],
  idPrefix: ["url", ServiceId],
  resolve(node, ctx) {
    resolveDefaultType(node, "Service");
    node.offers = resolveRelation(node.offers, ctx, offerResolver);
    node.aggregateRating = resolveRelation(node.aggregateRating, ctx, aggregateRatingResolver);
    node.review = resolveRelation(node.review, ctx, reviewResolver);
    return node;
  },
  resolveRootNode(service, { find }) {
    const webPage = find(PrimaryWebPageId);
    const identity = find(IdentityId);
    if (identity)
      setIfEmpty(service, "provider", idReference(identity));
    if (identity)
      setIfEmpty(service, "brand", idReference(identity));
    if (webPage)
      setIfEmpty(service, "mainEntityOfPage", idReference(webPage));
    return service;
  }
});

export { ServiceId, serviceResolver };
