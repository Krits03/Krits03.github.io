import { defineHeadPlugin, TemplateParamsPlugin } from 'unhead/plugins';
import { processTemplateParams } from 'unhead/utils';
import { hasProtocol, withBase, hasTrailingSlash, withTrailingSlash, withoutTrailingSlash, joinURL } from 'ufo';

function defineSchemaOrgResolver(schema) {
  return schema;
}

function idReference(node) {
  return {
    "@id": typeof node !== "string" ? node["@id"] : node
  };
}
function resolvableDateToDate(val) {
  try {
    const date = val instanceof Date ? val : new Date(Date.parse(val));
    const month = String(date.getMonth() + 1).padStart(2, "0");
    const day = String(date.getDate()).padStart(2, "0");
    return `${date.getFullYear()}-${month}-${day}`;
  } catch {
  }
  return typeof val === "string" ? val : val.toString();
}
const IS_VALID_W3C_DATE = [
  /(\d{4}-[01]\d-[0-3]\dT[0-2]\d:[0-5]\d:[0-5]\d\.\d+([+-][0-2]\d:[0-5]\d|Z))|(\d{4}-[01]\d-[0-3]\dT[0-2]\d:[0-5]\d:[0-5]\d([+-][0-2]\d:[0-5]\d|Z))|(\d{4}-[01]\d-[0-3]\dT[0-2]\d:[0-5]\d([+-][0-2]\d:[0-5]\d|Z))/,
  /^\d{4}-[01]\d-[0-3]\d$/,
  /^\d{4}-[01]\d$/,
  /^\d{4}$/
];
function isValidW3CDate(d) {
  return IS_VALID_W3C_DATE.some((r) => r.test(d));
}
function resolvableDateToIso(val) {
  if (!val)
    return val;
  try {
    if (val instanceof Date)
      return val.toISOString();
    else if (isValidW3CDate(val))
      return val;
    else
      return new Date(Date.parse(val)).toISOString();
  } catch {
  }
  return typeof val === "string" ? val : val.toString();
}
const IdentityId = "#identity";
function setIfEmpty(node, field, value) {
  if (!node?.[field] && value)
    node[field] = value;
}
function asArray(input) {
  return Array.isArray(input) ? input : [input];
}
function dedupeMerge(node, field, value) {
  const data = new Set(asArray(node[field]));
  data.add(value);
  node[field] = [...data].filter(Boolean);
}
function prefixId(url, id) {
  if (hasProtocol(id))
    return id;
  if (!id.includes("#"))
    id = `#${id}`;
  return `${url || ""}${id}`;
}
function trimLength(val, length) {
  if (!val)
    return val;
  if (val.length > length) {
    const trimmedString = val.substring(0, length);
    return trimmedString.substring(0, Math.min(trimmedString.length, trimmedString.lastIndexOf(" ")));
  }
  return val;
}
function resolveDefaultType(node, defaultType) {
  const val = node["@type"];
  if (val === defaultType)
    return;
  if (typeof val === "string" && typeof defaultType === "string") {
    if (val !== defaultType)
      node["@type"] = [defaultType, val];
    return;
  }
  const types = new Set(asArray(defaultType));
  for (const t of asArray(val)) {
    if (t != null)
      types.add(t);
  }
  const resolved = [...types];
  node["@type"] = resolved.length === 1 ? resolved[0] : resolved;
}
function resolveWithBase(base, urlOrPath) {
  if (!urlOrPath || hasProtocol(urlOrPath) || urlOrPath[0] !== "/" && urlOrPath[0] !== "#")
    return urlOrPath;
  return withBase(urlOrPath, base);
}
function resolveAsGraphKey(key) {
  if (!key)
    return key;
  return key.substring(key.lastIndexOf("#"));
}
function stripEmptyProperties(obj) {
  for (const k in obj) {
    if (!Object.prototype.hasOwnProperty.call(obj, k))
      continue;
    const v = obj[k];
    if (v === "" || v === null || v === void 0) {
      delete obj[k];
    } else if (typeof v === "object" && v !== null) {
      if (v.__v_isReadonly || v.__v_isRef)
        continue;
      stripEmptyProperties(v);
    }
  }
  return obj;
}

const imageResolver = defineSchemaOrgResolver({
  alias: "image",
  cast(input) {
    if (typeof input === "string") {
      input = {
        url: input
      };
    }
    return input;
  },
  defaults: {
    "@type": "ImageObject"
  },
  inheritMeta: [
    // @todo possibly only do if there's a caption
    "inLanguage"
  ],
  idPrefix: "host",
  resolve(image, { meta }) {
    image.url = resolveWithBase(meta.host, image.url);
    setIfEmpty(image, "contentUrl", image.url);
    if (image.height && !image.width)
      delete image.height;
    if (image.width && !image.height)
      delete image.width;
    return image;
  }
});

const index = {
  __proto__: null,
  imageResolver: imageResolver
};

function nextNodeId(ctx, alias) {
  ctx.nodeIdCounters[alias] = (ctx.nodeIdCounters[alias] || 0) + 1;
  return ctx.nodeIdCounters[alias].toString();
}
function resolveMeta(meta) {
  if (!meta.host && meta.canonicalHost)
    meta.host = meta.canonicalHost;
  if (!meta.tagPosition && meta.position)
    meta.tagPosition = meta.position;
  if (!meta.currency && meta.defaultCurrency)
    meta.currency = meta.defaultCurrency;
  if (!meta.inLanguage && meta.defaultLanguage)
    meta.inLanguage = meta.defaultLanguage;
  if (!meta.path)
    meta.path = "/";
  if (!meta.host && typeof document !== "undefined")
    meta.host = document.location.host;
  if (!meta.url && meta.canonicalUrl)
    meta.url = meta.canonicalUrl;
  if (meta.path !== "/") {
    if (meta.trailingSlash && !hasTrailingSlash(meta.path))
      meta.path = withTrailingSlash(meta.path);
    else if (!meta.trailingSlash && hasTrailingSlash(meta.path))
      meta.path = withoutTrailingSlash(meta.path);
  }
  meta.url = joinURL(meta.host || "", meta.path);
  return {
    ...meta,
    host: meta.host,
    url: meta.url,
    currency: meta.currency,
    image: meta.image,
    inLanguage: meta.inLanguage,
    title: meta.title,
    description: meta.description,
    datePublished: meta.datePublished,
    dateModified: meta.dateModified
  };
}
function resolveNode(node, ctx, resolver) {
  if (resolver?.cast)
    node = resolver.cast(node, ctx);
  if (resolver?.defaults) {
    let defaults = resolver.defaults;
    if (typeof defaults === "function")
      defaults = defaults(ctx);
    node = { ...defaults, ...node };
  }
  const inheritMeta = resolver?.inheritMeta;
  if (inheritMeta) {
    for (let i = 0; i < inheritMeta.length; i++) {
      const entry = inheritMeta[i];
      if (typeof entry === "string")
        setIfEmpty(node, entry, ctx.meta[entry]);
      else
        setIfEmpty(node, entry.key, ctx.meta[entry.meta]);
    }
  }
  if (resolver?.resolve)
    node = resolver.resolve(node, ctx);
  for (const k in node) {
    const v = node[k];
    if (Array.isArray(v)) {
      for (let i = 0; i < v.length; i++) {
        const item = v[i];
        if (typeof item === "object" && item?._resolver)
          node[k][i] = resolveRelation(item, ctx, item._resolver);
      }
    } else if (typeof v === "object" && v?._resolver) {
      node[k] = resolveRelation(v, ctx, v._resolver);
    }
  }
  stripEmptyProperties(node);
  return node;
}
function resolveNodeId(node, ctx, resolver, resolveAsRoot = false) {
  if (node["@id"] && node["@id"].startsWith("http"))
    return node;
  const prefix = resolver ? (Array.isArray(resolver.idPrefix) ? resolver.idPrefix[0] : resolver.idPrefix) || "url" : "url";
  const rootId = node["@id"] || (resolver ? Array.isArray(resolver.idPrefix) ? resolver.idPrefix?.[1] : void 0 : "");
  if (!node["@id"] && resolveAsRoot && rootId) {
    node["@id"] = prefixId(ctx.meta[prefix], rootId);
    return node;
  }
  if (node["@id"]?.startsWith("#/schema/") || node["@id"]?.startsWith("/")) {
    node["@id"] = prefixId(ctx.meta[prefix], node["@id"]);
    return node;
  }
  let alias = resolver?.alias;
  if (!alias) {
    const type = asArray(node["@type"])?.[0] || "";
    alias = type.replace(/([a-z])([A-Z])/g, "$1-$2").toLowerCase();
  }
  node["@id"] = prefixId(ctx.meta[prefix], `#/schema/${alias}/${node["@id"] || nextNodeId(ctx, alias)}`);
  return node;
}
function resolveRelation(input, ctx, fallbackResolver, options = {}) {
  if (!input)
    return input;
  const items = asArray(input);
  const ids = [];
  for (let i = 0; i < items.length; i++) {
    const a = items[i];
    let keyCount = 0;
    for (const _ in a) keyCount++;
    if (keyCount === 1 && a["@id"] || keyCount === 2 && a["@id"] && a["@type"]) {
      ids.push(resolveNodeId({
        "@id": ctx.find(a["@id"])?.["@id"] || a["@id"]
      }, ctx));
      continue;
    }
    let resolver = fallbackResolver;
    if (a._resolver && typeof a._resolver !== "string") {
      resolver = a._resolver;
      delete a._resolver;
    }
    if (!resolver) {
      ids.push(a);
      continue;
    }
    let node = resolveNode(a, ctx, resolver);
    if (options.afterResolve)
      options.afterResolve(node);
    if (options.generateId || options.root)
      node = resolveNodeId(node, ctx, resolver, false);
    if (options.root) {
      if (resolver.resolveRootNode)
        resolver.resolveRootNode(node, ctx);
      ctx.push(node);
      ids.push(idReference(node["@id"]));
      continue;
    }
    ids.push(node);
  }
  return !options.array && ids.length === 1 ? ids[0] : ids;
}

const UNSAFE_KEYS$1 = /* @__PURE__ */ new Set(["__proto__", "constructor", "prototype"]);
function merge(target, source) {
  if (!source)
    return target;
  for (const key in source) {
    if (!Object.prototype.hasOwnProperty.call(source, key) || UNSAFE_KEYS$1.has(key))
      continue;
    const value = source[key];
    if (value === void 0)
      continue;
    if (Array.isArray(target[key])) {
      if (Array.isArray(value)) {
        const merged = [...target[key], ...value];
        if (key === "@type") {
          target[key] = [...new Set(merged)];
        } else if (key === "itemListElement") {
          merged.sort((a, b) => (a.position || 0) - (b.position || 0));
          for (let i = 0; i < merged.length; i++)
            merged[i].position = i + 1;
          target[key] = merged;
        } else if (key === "potentialAction") {
          const byType = /* @__PURE__ */ Object.create(null);
          for (const action of merged) {
            const type = action["@type"];
            if (byType[type]) {
              if (action.target && byType[type].target) {
                const a = Array.isArray(byType[type].target) ? byType[type].target : [byType[type].target];
                const b = Array.isArray(action.target) ? action.target : [action.target];
                byType[type].target = [.../* @__PURE__ */ new Set([...a, ...b])];
              }
            } else {
              byType[type] = { ...action };
            }
          }
          target[key] = Object.values(byType);
        } else {
          target[key] = merged;
        }
      } else {
        target[key] = merge(target[key], [value]);
      }
    } else if (target[key] && typeof target[key] === "object" && typeof value === "object" && !Array.isArray(value)) {
      target[key] = merge({ ...target[key] }, value);
    } else {
      target[key] = value;
    }
  }
  return target;
}

function indexNode(index, node) {
  if (!node["@id"])
    return;
  const nodeId = node["@id"];
  const fragmentKey = resolveAsGraphKey(nodeId);
  index.set(fragmentKey, node);
  index.set(nodeId, node);
  const domainKey = nodeId.replace(/(https?:)?\/\//, "").split("/")[0];
  index.set(domainKey, node);
}
function createSchemaOrgGraph() {
  const ctx = {
    find(id) {
      let resolver = (s) => s;
      if (id[0] === "#") {
        resolver = resolveAsGraphKey;
      } else if (id[0] === "/") {
        resolver = (s) => s.replace(/(https?:)?\/\//, "").split("/")[0];
      }
      const key = resolver(id);
      if (ctx.nodeIndex.size > 0) {
        return ctx.nodeIndex.get(key) || null;
      }
      return ctx.nodes.filter((n) => !!n["@id"]).find((n) => resolver(n["@id"]) === key);
    },
    push(input) {
      asArray(input).forEach((node) => {
        const registeredNode = node;
        ctx.nodes.push(registeredNode);
        if (ctx.nodeIndex.size > 0)
          indexNode(ctx.nodeIndex, registeredNode);
      });
    },
    resolveGraph(meta) {
      for (const k in ctx.nodeIdCounters) delete ctx.nodeIdCounters[k];
      ctx.meta = resolveMeta({ ...meta });
      const len = ctx.nodes.length;
      for (let i = 0; i < len; i++) {
        let node = ctx.nodes[i];
        const resolver = node._resolver;
        node = resolveNode(node, ctx, resolver);
        node = resolveNodeId(node, ctx, resolver, true);
        ctx.nodes[i] = node;
      }
      const dedupedNodes = /* @__PURE__ */ Object.create(null);
      ctx.nodeIndex = /* @__PURE__ */ new Map();
      for (let i = 0; i < ctx.nodes.length; i++) {
        const n = ctx.nodes[i];
        const nodeKey = resolveAsGraphKey(n["@id"]);
        if (dedupedNodes[nodeKey]) {
          if (n._dedupeStrategy !== "replace")
            dedupedNodes[nodeKey] = merge(dedupedNodes[nodeKey], n);
          else
            dedupedNodes[nodeKey] = n;
        } else {
          dedupedNodes[nodeKey] = n;
        }
      }
      ctx.nodes = Object.values(dedupedNodes);
      for (let i = 0; i < ctx.nodes.length; i++)
        indexNode(ctx.nodeIndex, ctx.nodes[i]);
      const countBeforeRelations = ctx.nodes.length;
      for (let i = 0; i < ctx.nodes.length; i++) {
        const node = ctx.nodes[i];
        if (node.image && typeof node.image === "string") {
          node.image = resolveRelation(node.image, ctx, imageResolver, {
            root: true
          });
        }
        node.translationOfWork = resolveRelation(node.translationOfWork, ctx);
        node.workTranslation = resolveRelation(node.workTranslation, ctx);
        if (node._resolver?.resolveRootNode)
          node._resolver.resolveRootNode(node, ctx);
        delete node._resolver;
      }
      const needsDedupe = ctx.nodes.length > countBeforeRelations;
      const normalizedNodes = needsDedupe ? /* @__PURE__ */ Object.create(null) : null;
      const result = needsDedupe ? null : [];
      for (let i = 0; i < ctx.nodes.length; i++) {
        const n = ctx.nodes[i];
        const nodeKey = resolveAsGraphKey(n["@id"]);
        const keys = Object.keys(n);
        const primitives = [];
        const relations = [];
        for (let j = 0; j < keys.length; j++) {
          const k = keys[j];
          if (k[0] === "_")
            continue;
          const v = n[k];
          if (v !== null && (Array.isArray(v) || typeof v === "object"))
            relations.push(k);
          else
            primitives.push(k);
        }
        primitives.sort();
        relations.sort();
        const newNode = {};
        for (let j = 0; j < primitives.length; j++)
          newNode[primitives[j]] = n[primitives[j]];
        for (let j = 0; j < relations.length; j++)
          newNode[relations[j]] = n[relations[j]];
        if (needsDedupe) {
          normalizedNodes[nodeKey] = normalizedNodes[nodeKey] ? merge(normalizedNodes[nodeKey], newNode) : newNode;
        } else {
          result.push(newNode);
        }
      }
      return needsDedupe ? Object.values(normalizedNodes) : result;
    },
    nodes: [],
    nodeIndex: /* @__PURE__ */ new Map(),
    nodeIdCounters: /* @__PURE__ */ Object.create(null),
    meta: {}
  };
  return ctx;
}

const resolverCache = {};
const resolverImports = {
  address: () => import('../chunks/index28.mjs'),
  aggregateOffer: () => import('../chunks/index.mjs'),
  aggregateRating: () => import('../chunks/index2.mjs'),
  article: () => import('../chunks/index3.mjs').then(function (n) { return n.l; }),
  breadcrumb: () => import('../chunks/index3.mjs').then(function (n) { return n.i; }),
  comment: () => import('../chunks/index5.mjs'),
  course: () => import('../chunks/index6.mjs'),
  dataset: () => import('../chunks/index7.mjs'),
  event: () => import('../chunks/index10.mjs'),
  foodEstablishment: () => import('../chunks/index11.mjs'),
  virtualLocation: () => import('../chunks/index9.mjs'),
  place: () => import('../chunks/index8.mjs'),
  howTo: () => import('../chunks/index13.mjs'),
  howToStep: () => import('../chunks/index12.mjs').then(function (n) { return n.i; }),
  image: () => Promise.resolve().then(function () { return index; }),
  localBusiness: () => import('../chunks/index17.mjs'),
  offer: () => import('../chunks/index23.mjs'),
  openingHours: () => import('../chunks/index24.mjs'),
  organization: () => import('../chunks/index3.mjs').then(function (n) { return n.h; }),
  person: () => import('../chunks/index3.mjs').then(function (n) { return n.k; }),
  product: () => import('../chunks/index29.mjs'),
  question: () => import('../chunks/index30.mjs'),
  recipe: () => import('../chunks/index31.mjs'),
  review: () => import('../chunks/index32.mjs'),
  video: () => import('../chunks/index38.mjs'),
  webPage: () => import('../chunks/index3.mjs').then(function (n) { return n.j; }),
  webSite: () => import('../chunks/index3.mjs').then(function (n) { return n.g; }),
  book: () => import('../chunks/index4.mjs'),
  itemList: () => import('../chunks/index14.mjs'),
  jobPosting: () => import('../chunks/index15.mjs'),
  listItem: () => import('../chunks/index16.mjs'),
  movie: () => import('../chunks/index18.mjs'),
  musicAlbum: () => import('../chunks/index19.mjs'),
  musicGroup: () => import('../chunks/index20.mjs'),
  musicPlaylist: () => import('../chunks/index21.mjs'),
  musicRecording: () => import('../chunks/index22.mjs'),
  podcastEpisode: () => import('../chunks/index25.mjs'),
  podcastSeason: () => import('../chunks/index26.mjs'),
  podcastSeries: () => import('../chunks/index27.mjs'),
  searchAction: () => import('../chunks/index40.mjs'),
  readAction: () => import('../chunks/index39.mjs'),
  service: () => import('../chunks/index33.mjs'),
  softwareApp: () => import('../chunks/index34.mjs'),
  tvEpisode: () => import('../chunks/index35.mjs'),
  tvSeason: () => import('../chunks/index36.mjs'),
  tvSeries: () => import('../chunks/index37.mjs'),
  bookEdition: () => import('../chunks/index4.mjs')
};
const resolverExportNames = {
  address: "addressResolver",
  aggregateOffer: "aggregateOfferResolver",
  aggregateRating: "aggregateRatingResolver",
  article: "articleResolver",
  breadcrumb: "breadcrumbResolver",
  comment: "commentResolver",
  course: "courseResolver",
  dataset: "datasetResolver",
  event: "eventResolver",
  foodEstablishment: "foodEstablishmentResolver",
  virtualLocation: "virtualLocationResolver",
  place: "placeResolver",
  howTo: "howToResolver",
  howToStep: "howToStepResolver",
  image: "imageResolver",
  localBusiness: "localBusinessResolver",
  offer: "offerResolver",
  openingHours: "openingHoursResolver",
  organization: "organizationResolver",
  person: "personResolver",
  product: "productResolver",
  question: "questionResolver",
  recipe: "recipeResolver",
  review: "reviewResolver",
  video: "videoResolver",
  webPage: "webPageResolver",
  webSite: "webSiteResolver",
  book: "bookResolver",
  itemList: "itemListResolver",
  jobPosting: "jobPostingResolver",
  listItem: "listItemResolver",
  movie: "movieResolver",
  musicAlbum: "musicAlbumResolver",
  musicGroup: "musicGroupResolver",
  musicPlaylist: "musicPlaylistResolver",
  musicRecording: "musicRecordingResolver",
  podcastEpisode: "podcastEpisodeResolver",
  podcastSeason: "podcastSeasonResolver",
  podcastSeries: "podcastSeriesResolver",
  searchAction: "searchActionResolver",
  readAction: "readActionResolver",
  service: "serviceResolver",
  softwareApp: "softwareAppResolver",
  tvEpisode: "tvEpisodeResolver",
  tvSeason: "tvSeasonResolver",
  tvSeries: "tvSeriesResolver",
  bookEdition: "bookEditionResolver"
};
async function loadResolver(resolver) {
  if (resolverCache[resolver])
    return resolverCache[resolver];
  const importFn = resolverImports[resolver];
  if (!importFn)
    return null;
  const mod = await importFn();
  const exportName = resolverExportNames[resolver];
  const loaded = mod[exportName] || mod.default;
  if (loaded)
    resolverCache[resolver] = loaded;
  return loaded || null;
}

const UNSAFE_KEYS = /* @__PURE__ */ new Set(["__proto__", "constructor", "prototype"]);
async function preloadNestedResolvers(obj) {
  if (!obj || typeof obj !== "object")
    return;
  const promises = [];
  if (typeof obj._resolver === "string") {
    const resolverName = obj._resolver;
    promises.push(loadResolver(resolverName).then((loaded) => {
      if (loaded)
        obj._resolver = loaded;
    }));
  }
  for (const key in obj) {
    if (!Object.prototype.hasOwnProperty.call(obj, key) || UNSAFE_KEYS.has(key))
      continue;
    const val = obj[key];
    if (val && typeof val === "object") {
      if (Array.isArray(val)) {
        for (const item of val) {
          promises.push(preloadNestedResolvers(item));
        }
      } else {
        promises.push(preloadNestedResolvers(val));
      }
    }
  }
  await Promise.all(promises);
}
function mergeObjects(target, source) {
  const result = { ...target };
  for (const key in source) {
    if (!Object.prototype.hasOwnProperty.call(source, key) || source[key] === void 0 || UNSAFE_KEYS.has(key))
      continue;
    const isNestedObject = result[key] && typeof result[key] === "object" && typeof source[key] === "object" && !Array.isArray(result[key]) && !Array.isArray(source[key]);
    if (isNestedObject)
      result[key] = mergeObjects(result[key], source[key]);
    else if (!result[key])
      result[key] = source[key];
  }
  return result;
}
function UnheadSchemaOrg(options) {
  return SchemaOrgUnheadPlugin({}, () => ({}), options);
}
function PluginSchemaOrg(options) {
  const fallback = () => ({});
  return SchemaOrgUnheadPlugin({}, options?.resolveMeta || fallback, options);
}
function SchemaOrgUnheadPlugin(config, meta, options) {
  config = resolveMeta({ ...config });
  let graph;
  let resolvedMeta = {};
  return defineHeadPlugin((head) => {
    head.use(TemplateParamsPlugin);
    return {
      key: "schema-org",
      hooks: {
        "entries:normalize": async ({ tags }) => {
          graph = graph || createSchemaOrgGraph();
          for (const tag of tags) {
            if (tag.tag === "script" && tag.props.type === "application/ld+json" && tag.props.nodes) {
              const nodes = await tag.props.nodes;
              for (const node of Array.isArray(nodes) ? nodes : [nodes]) {
                if (typeof node !== "object" || Object.keys(node).length === 0) {
                  continue;
                }
                await preloadNestedResolvers(node);
                const newNode = {
                  ...node,
                  _dedupeStrategy: tag.tagDuplicateStrategy
                };
                graph.push(newNode);
              }
              tag.tagPosition = tag.tagPosition || config.tagPosition === "head" ? "head" : "bodyClose";
            }
            if (tag.tag === "htmlAttrs" && tag.props.lang) {
              resolvedMeta.inLanguage = tag.props.lang;
            } else if (tag.tag === "title") {
              resolvedMeta.title = tag.textContent;
            } else if (tag.tag === "meta" && tag.props.name === "description") {
              resolvedMeta.description = tag.props.content;
            } else if (tag.tag === "link" && tag.props.rel === "canonical") {
              resolvedMeta.url = tag.props.href;
              if (resolvedMeta.url && !resolvedMeta.host) {
                try {
                  resolvedMeta.host = new URL(resolvedMeta.url).origin;
                } catch {
                }
              }
            } else if (tag.tag === "meta" && tag.props.property === "og:image") {
              resolvedMeta.image = tag.props.content;
            } else if (tag.tag === "templateParams" && tag.props.schemaOrg) {
              resolvedMeta = {
                ...resolvedMeta,
                // @ts-expect-error untyped
                ...tag.props.schemaOrg
              };
              delete tag.props.schemaOrg;
            }
          }
        },
        "tags:resolve": async (ctx) => {
          for (const k in ctx.tags) {
            const tag = ctx.tags[k];
            if (tag.tag === "script" && tag.props.type === "application/ld+json" && tag.props.nodes) {
              delete tag.props.nodes;
              const resolvedGraph = graph.resolveGraph({ ...await meta?.() || {}, ...config, ...resolvedMeta });
              if (!resolvedGraph.length) {
                tag.props = {};
                return;
              }
              const minify = options?.minify || process.env.NODE_ENV === "production";
              tag.innerHTML = JSON.stringify({
                "@context": "https://schema.org",
                "@graph": resolvedGraph
              }, (_, value) => {
                if (typeof value !== "object")
                  return processTemplateParams(value, head._templateParams, head._separator);
                return value;
              }, minify ? 0 : 2);
              return;
            }
          }
        },
        "tags:afterResolve": (ctx) => {
          let firstNodeKey;
          for (const k in ctx.tags) {
            const tag = ctx.tags[k];
            if (!tag?.props)
              continue;
            if (tag.props.type === "application/ld+json" && tag.props.nodes || tag.key === "schema-org-graph") {
              delete tag.props.nodes;
              if (typeof firstNodeKey === "undefined") {
                firstNodeKey = k;
                continue;
              }
              ctx.tags[firstNodeKey].props = mergeObjects(ctx.tags[firstNodeKey].props, tag.props);
              delete ctx.tags[firstNodeKey].props.nodes;
              ctx.tags[k] = false;
            }
          }
          ctx.tags = ctx.tags.filter(Boolean);
        }
      }
    };
  });
}

function provideResolver(input, resolver) {
  if (!input)
    input = {};
  input._resolver = resolver;
  return input;
}
function defineAddress(input) {
  return provideResolver(input, "address");
}
function defineAggregateOffer(input) {
  return provideResolver(input, "aggregateOffer");
}
function defineAggregateRating(input) {
  return provideResolver(input, "aggregateRating");
}
function defineArticle(input) {
  return provideResolver(input, "article");
}
function defineBreadcrumb(input) {
  return provideResolver(input, "breadcrumb");
}
function defineComment(input) {
  return provideResolver(input, "comment");
}
function defineEvent(input) {
  return provideResolver(input, "event");
}
function defineFoodEstablishment(input) {
  return provideResolver(input, "foodEstablishment");
}
function defineVirtualLocation(input) {
  return provideResolver(input, "virtualLocation");
}
function definePlace(input) {
  return provideResolver(input, "place");
}
function defineHowTo(input) {
  return provideResolver(input, "howTo");
}
function defineHowToStep(input) {
  return provideResolver(input, "howToStep");
}
function defineImage(input) {
  return provideResolver(input, "image");
}
function defineJobPosting(input) {
  return provideResolver(input, "jobPosting");
}
function defineLocalBusiness(input) {
  return provideResolver(input, "localBusiness");
}
function defineOffer(input) {
  return provideResolver(input, "offer");
}
function defineOpeningHours(input) {
  return provideResolver(input, "openingHours");
}
function defineOrganization(input) {
  return provideResolver(input, "organization");
}
function definePerson(input) {
  return provideResolver(input, "person");
}
function defineProduct(input) {
  return provideResolver(input, "product");
}
function defineQuestion(input) {
  return provideResolver(input, "question");
}
function defineRecipe(input) {
  return provideResolver(input, "recipe");
}
function defineReview(input) {
  return provideResolver(input, "review");
}
function defineVideo(input) {
  return provideResolver(input, "video");
}
function defineWebPage(input) {
  return provideResolver(input, "webPage");
}
function defineWebSite(input) {
  return provideResolver(input, "webSite");
}
function defineBook(input) {
  return provideResolver(input, "book");
}
function defineCourse(input) {
  return provideResolver(input, "course");
}
function defineItemList(input) {
  return provideResolver(input, "itemList");
}
function defineListItem(input) {
  return provideResolver(input, "listItem");
}
function defineMovie(input) {
  return provideResolver(input, "movie");
}
function defineSearchAction(input) {
  return provideResolver(input, "searchAction");
}
function defineReadAction(input) {
  return provideResolver(input, "readAction");
}
function defineDataset(input) {
  return provideResolver(input, "dataset");
}
function defineMusicRecording(input) {
  return provideResolver(input, "musicRecording");
}
function defineMusicAlbum(input) {
  return provideResolver(input, "musicAlbum");
}
function defineMusicGroup(input) {
  return provideResolver(input, "musicGroup");
}
function defineMusicPlaylist(input) {
  return provideResolver(input, "musicPlaylist");
}
function definePodcastSeries(input) {
  return provideResolver(input, "podcastSeries");
}
function definePodcastEpisode(input) {
  return provideResolver(input, "podcastEpisode");
}
function definePodcastSeason(input) {
  return provideResolver(input, "podcastSeason");
}
function defineTVSeries(input) {
  return provideResolver(input, "tvSeries");
}
function defineTVSeason(input) {
  return provideResolver(input, "tvSeason");
}
function defineTVEpisode(input) {
  return provideResolver(input, "tvEpisode");
}
function defineService(input) {
  return provideResolver(input, "service");
}
function defineSoftwareApp(input) {
  return provideResolver(input, "softwareApp");
}
function defineBookEdition(input) {
  return provideResolver(input, "bookEdition");
}
function normalizeSchemaOrgInput(input) {
  if (input.script) {
    return input;
  }
  return {
    script: [
      {
        type: "application/ld+json",
        key: "schema-org-graph",
        nodes: input
      }
    ]
  };
}
function useSchemaOrg(unhead, input = [], options = {}) {
  unhead.use(UnheadSchemaOrg());
  const entry = unhead.push(normalizeSchemaOrgInput(input), options);
  const corePatch = entry.patch;
  entry.patch = (input2) => corePatch(normalizeSchemaOrgInput(input2));
  return entry;
}

export { defineVideo as $, defineMovie as A, defineMusicAlbum as B, defineMusicGroup as C, defineMusicPlaylist as D, defineMusicRecording as E, defineOffer as F, defineOpeningHours as G, defineOrganization as H, definePerson as I, definePlace as J, definePodcastEpisode as K, definePodcastSeason as L, definePodcastSeries as M, defineProduct as N, defineQuestion as O, PluginSchemaOrg as P, defineReadAction as Q, defineRecipe as R, SchemaOrgUnheadPlugin as S, defineReview as T, UnheadSchemaOrg as U, defineSearchAction as V, defineService as W, defineSoftwareApp as X, defineTVEpisode as Y, defineTVSeason as Z, defineTVSeries as _, resolveNode as a, defineVirtualLocation as a0, defineWebPage as a1, defineWebSite as a2, normalizeSchemaOrgInput as a3, useSchemaOrg as a4, imageResolver as a5, setIfEmpty as a6, idReference as a7, resolvableDateToIso as a8, IdentityId as a9, resolveDefaultType as aa, resolvableDateToDate as ab, asArray as ac, resolveWithBase as ad, dedupeMerge as ae, resolveAsGraphKey as af, prefixId as ag, trimLength as ah, resolveNodeId as b, createSchemaOrgGraph as c, defineSchemaOrgResolver as d, resolveRelation as e, defineAddress as f, defineAggregateOffer as g, defineAggregateRating as h, defineArticle as i, defineBook as j, defineBookEdition as k, defineBreadcrumb as l, merge as m, defineComment as n, defineCourse as o, defineDataset as p, defineEvent as q, resolveMeta as r, defineFoodEstablishment as s, defineHowTo as t, defineHowToStep as u, defineImage as v, defineItemList as w, defineJobPosting as x, defineListItem as y, defineLocalBusiness as z };
