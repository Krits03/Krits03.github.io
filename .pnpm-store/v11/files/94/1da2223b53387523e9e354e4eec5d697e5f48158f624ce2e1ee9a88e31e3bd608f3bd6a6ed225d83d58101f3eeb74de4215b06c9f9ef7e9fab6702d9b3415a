import { d as defineSchemaOrgResolver, a8 as resolvableDateToIso, ad as resolveWithBase, e as resolveRelation } from '../shared/schema-org.BygE6hLl.mjs';
import { aggregateRatingResolver } from './index2.mjs';
import { p as personResolver } from './index3.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';

const musicPlaylistResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "MusicPlaylist"
  },
  idPrefix: "host",
  resolve(node, ctx) {
    if (node.datePublished)
      node.datePublished = resolvableDateToIso(node.datePublished);
    if (node.dateModified)
      node.dateModified = resolvableDateToIso(node.dateModified);
    if (node.url)
      node.url = resolveWithBase(ctx.meta.host, node.url);
    node.creator = resolveRelation(node.creator, ctx, personResolver);
    node.aggregateRating = resolveRelation(node.aggregateRating, ctx, aggregateRatingResolver);
    return node;
  }
});

export { musicPlaylistResolver };
