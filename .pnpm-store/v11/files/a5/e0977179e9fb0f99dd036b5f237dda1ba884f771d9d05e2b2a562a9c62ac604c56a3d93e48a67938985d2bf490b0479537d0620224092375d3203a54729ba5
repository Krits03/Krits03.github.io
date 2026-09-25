import { p as personResolver } from './index3.mjs';
import { r as ratingResolver } from '../shared/schema-org.SD01-lvP.mjs';
import { d as defineSchemaOrgResolver, e as resolveRelation } from '../shared/schema-org.BygE6hLl.mjs';
import 'ufo';
import './index16.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';

const reviewResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "Review"
  },
  inheritMeta: [
    "inLanguage"
  ],
  resolve(review, ctx) {
    review.reviewRating = resolveRelation(review.reviewRating, ctx, ratingResolver);
    review.author = resolveRelation(review.author, ctx, personResolver);
    return review;
  }
});

export { reviewResolver };
