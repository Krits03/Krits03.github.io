import { d as defineSchemaOrgResolver, a6 as setIfEmpty, a7 as idReference, e as resolveRelation } from '../shared/schema-org.BygE6hLl.mjs';
import { P as PrimaryArticleId, d as PrimaryWebPageId } from './index3.mjs';
import { h as howToStepResolver } from './index12.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';

const RecipeId = "#recipe";
const recipeResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "Recipe"
  },
  inheritMeta: [
    { meta: "title", key: "name" },
    "description",
    "image",
    "datePublished"
  ],
  idPrefix: ["url", RecipeId],
  resolve(node, ctx) {
    node.recipeInstructions = resolveRelation(node.recipeInstructions, ctx, howToStepResolver);
    return node;
  },
  resolveRootNode(node, { find }) {
    const article = find(PrimaryArticleId);
    const webPage = find(PrimaryWebPageId);
    if (article)
      setIfEmpty(node, "mainEntityOfPage", idReference(article));
    else if (webPage)
      setIfEmpty(node, "mainEntityOfPage", idReference(webPage));
    if (article?.author)
      setIfEmpty(node, "author", article.author);
    return node;
  }
});

export { RecipeId, recipeResolver };
