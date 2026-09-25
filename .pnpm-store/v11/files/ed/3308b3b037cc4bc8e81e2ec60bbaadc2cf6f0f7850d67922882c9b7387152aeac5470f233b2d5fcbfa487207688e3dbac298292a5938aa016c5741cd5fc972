import { d as defineSchemaOrgResolver, e as resolveRelation, a8 as resolvableDateToIso } from '../shared/schema-org.BygE6hLl.mjs';
import { aggregateRatingResolver } from './index2.mjs';
import { p as personResolver, o as organizationResolver } from './index3.mjs';
import { videoResolver } from './index38.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';

const tvSeasonResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "TVSeason"
  },
  resolve(node, ctx) {
    node.actor = resolveRelation(node.actor, ctx, personResolver);
    node.director = resolveRelation(node.director, ctx, personResolver);
    node.productionCompany = resolveRelation(node.productionCompany, ctx, organizationResolver);
    node.aggregateRating = resolveRelation(node.aggregateRating, ctx, aggregateRatingResolver);
    node.trailer = resolveRelation(node.trailer, ctx, videoResolver);
    if (node.datePublished)
      node.datePublished = resolvableDateToIso(node.datePublished);
    if (node.startDate)
      node.startDate = resolvableDateToIso(node.startDate);
    if (node.endDate)
      node.endDate = resolvableDateToIso(node.endDate);
    return node;
  }
});

export { tvSeasonResolver };
