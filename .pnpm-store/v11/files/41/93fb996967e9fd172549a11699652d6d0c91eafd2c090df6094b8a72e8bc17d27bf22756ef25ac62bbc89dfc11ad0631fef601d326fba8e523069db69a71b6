import { d as defineSchemaOrgResolver, e as resolveRelation, a8 as resolvableDateToIso } from '../shared/schema-org.BygE6hLl.mjs';
import { aggregateRatingResolver } from './index2.mjs';
import { p as personResolver } from './index3.mjs';
import { reviewResolver } from './index32.mjs';
import { videoResolver } from './index38.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';
import '../shared/schema-org.SD01-lvP.mjs';

const tvEpisodeResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "TVEpisode"
  },
  resolve(node, ctx) {
    node.actor = resolveRelation(node.actor, ctx, personResolver);
    node.director = resolveRelation(node.director, ctx, personResolver);
    node.musicBy = resolveRelation(node.musicBy, ctx, personResolver);
    node.video = resolveRelation(node.video, ctx, videoResolver);
    node.aggregateRating = resolveRelation(node.aggregateRating, ctx, aggregateRatingResolver);
    node.review = resolveRelation(node.review, ctx, reviewResolver);
    if (node.datePublished)
      node.datePublished = resolvableDateToIso(node.datePublished);
    if (node.uploadDate)
      node.uploadDate = resolvableDateToIso(node.uploadDate);
    return node;
  }
});

export { tvEpisodeResolver };
