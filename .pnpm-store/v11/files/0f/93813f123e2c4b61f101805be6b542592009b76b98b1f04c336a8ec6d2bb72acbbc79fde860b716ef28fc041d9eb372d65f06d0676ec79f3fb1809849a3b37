import { d as defineSchemaOrgResolver, ab as resolvableDateToDate, ad as resolveWithBase, e as resolveRelation } from '../shared/schema-org.BygE6hLl.mjs';
import { p as personResolver } from './index3.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';

const musicGroupResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "MusicGroup"
  },
  idPrefix: "host",
  inheritMeta: [
    { meta: "host", key: "url" }
  ],
  resolve(node, ctx) {
    if (node.foundingDate)
      node.foundingDate = resolvableDateToDate(node.foundingDate);
    if (node.dissolutionDate)
      node.dissolutionDate = resolvableDateToDate(node.dissolutionDate);
    if (node.url)
      node.url = resolveWithBase(ctx.meta.host, node.url);
    node.member = resolveRelation(node.member, ctx, personResolver);
    return node;
  }
});

export { musicGroupResolver };
