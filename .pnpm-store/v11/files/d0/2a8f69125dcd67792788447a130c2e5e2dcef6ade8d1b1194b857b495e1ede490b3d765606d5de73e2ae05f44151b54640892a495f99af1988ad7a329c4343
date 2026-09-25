import { d as defineSchemaOrgResolver, e as resolveRelation, a8 as resolvableDateToIso } from '../shared/schema-org.BygE6hLl.mjs';
import { aggregateRatingResolver } from './index2.mjs';
import { p as personResolver } from './index3.mjs';
import { reviewResolver } from './index32.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';
import '../shared/schema-org.SD01-lvP.mjs';

const podcastEpisodeResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "PodcastEpisode"
  },
  inheritMeta: [
    "inLanguage"
  ],
  resolve(node, ctx) {
    node.author = resolveRelation(node.author, ctx, personResolver);
    node.aggregateRating = resolveRelation(node.aggregateRating, ctx, aggregateRatingResolver);
    node.review = resolveRelation(node.review, ctx, reviewResolver);
    if (node.datePublished)
      node.datePublished = resolvableDateToIso(node.datePublished);
    if (node.uploadDate)
      node.uploadDate = resolvableDateToIso(node.uploadDate);
    return node;
  }
});

export { podcastEpisodeResolver };
