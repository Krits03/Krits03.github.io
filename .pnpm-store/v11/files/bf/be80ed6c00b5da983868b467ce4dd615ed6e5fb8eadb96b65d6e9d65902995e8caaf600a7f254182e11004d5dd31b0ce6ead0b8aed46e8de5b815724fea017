import { d as defineSchemaOrgResolver, a6 as setIfEmpty, a7 as idReference, e as resolveRelation, a8 as resolvableDateToIso } from '../shared/schema-org.BygE6hLl.mjs';
import { P as PrimaryArticleId, p as personResolver } from './index3.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';

const commentResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "Comment"
  },
  idPrefix: "url",
  resolve(node, ctx) {
    node.author = resolveRelation(node.author, ctx, personResolver, {
      root: true
    });
    node.dateCreated = resolvableDateToIso(node.dateCreated);
    node.dateModified = resolvableDateToIso(node.dateModified);
    return node;
  },
  resolveRootNode(node, { find }) {
    const article = find(PrimaryArticleId);
    if (article)
      setIfEmpty(node, "about", idReference(article));
  }
});

export { commentResolver };
