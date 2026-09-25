import { d as defineSchemaOrgResolver, a8 as resolvableDateToIso, ad as resolveWithBase, e as resolveRelation } from '../shared/schema-org.BygE6hLl.mjs';
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

const musicAlbumResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "MusicAlbum"
  },
  idPrefix: "host",
  resolve(node, ctx) {
    if (node.datePublished)
      node.datePublished = resolvableDateToIso(node.datePublished);
    if (node.url)
      node.url = resolveWithBase(ctx.meta.host, node.url);
    node.byArtist = resolveRelation(node.byArtist, ctx, personResolver);
    node.aggregateRating = resolveRelation(node.aggregateRating, ctx, aggregateRatingResolver);
    node.review = resolveRelation(node.review, ctx, reviewResolver);
    return node;
  }
});

export { musicAlbumResolver };
