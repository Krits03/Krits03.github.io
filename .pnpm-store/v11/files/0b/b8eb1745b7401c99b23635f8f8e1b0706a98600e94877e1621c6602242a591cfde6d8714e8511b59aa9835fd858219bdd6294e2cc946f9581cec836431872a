import { d as defineSchemaOrgResolver, aa as resolveDefaultType, e as resolveRelation, a8 as resolvableDateToIso } from '../shared/schema-org.BygE6hLl.mjs';
import { p as personResolver } from './index3.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';
import './index16.mjs';
import './index28.mjs';
import './index40.mjs';
import './index39.mjs';

const PrimaryDatasetId = "#dataset";
const datasetResolver = defineSchemaOrgResolver({
  defaults: {
    "@type": "Dataset"
  },
  inheritMeta: [
    "description",
    "url",
    "dateModified",
    "datePublished",
    { meta: "title", key: "name" }
  ],
  idPrefix: ["url", PrimaryDatasetId],
  resolve(node, ctx) {
    resolveDefaultType(node, "Dataset");
    node.creator = resolveRelation(node.creator, ctx, personResolver, {
      root: true
    });
    node.dateModified = resolvableDateToIso(node.dateModified);
    node.datePublished = resolvableDateToIso(node.datePublished);
    return node;
  }
});

export { PrimaryDatasetId, datasetResolver };
