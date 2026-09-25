import { d as defineSchemaOrgResolver, a6 as setIfEmpty, a7 as idReference, e as resolveRelation } from '../shared/schema-org.BygE6hLl.mjs';
import { d as PrimaryWebPageId } from './index3.mjs';
import { h as howToStepResolver } from './index12.mjs';
export { a as howToStepDirectionResolver } from './index12.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';

const HowToId = "#howto";
const howToResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "HowTo"
  },
  inheritMeta: [
    "description",
    "image",
    "inLanguage",
    { meta: "title", key: "name" }
  ],
  idPrefix: ["url", HowToId],
  resolve(node, ctx) {
    node.step = resolveRelation(node.step, ctx, howToStepResolver);
    return node;
  },
  resolveRootNode(node, { find }) {
    const webPage = find(PrimaryWebPageId);
    if (webPage)
      setIfEmpty(node, "mainEntityOfPage", idReference(webPage));
  }
});

export { HowToId, howToResolver, howToStepResolver };
