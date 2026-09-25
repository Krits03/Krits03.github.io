import { d as defineSchemaOrgResolver, ac as asArray, a6 as setIfEmpty, a8 as resolvableDateToIso, ad as resolveWithBase, e as resolveRelation, a5 as imageResolver } from '../shared/schema-org.BygE6hLl.mjs';
import 'unhead/plugins';
import 'unhead/utils';
import 'ufo';

const videoResolver = defineSchemaOrgResolver({
  cast(input) {
    if (typeof input === "string") {
      input = {
        url: input
      };
    }
    return input;
  },
  alias: "video",
  defaults: {
    "@type": "VideoObject"
  },
  inheritMeta: [
    { meta: "title", key: "name" },
    "description",
    "image",
    "inLanguage",
    { meta: "datePublished", key: "uploadDate" }
  ],
  idPrefix: "host",
  resolve(video, ctx) {
    if (video.uploadDate)
      video.uploadDate = resolvableDateToIso(video.uploadDate);
    video.url = resolveWithBase(ctx.meta.host, video.url);
    if (video.caption && !video.description)
      video.description = video.caption;
    if (!video.description)
      video.description = "No description";
    if (video.thumbnailUrl && (typeof video.thumbnailUrl === "string" || Array.isArray(video.thumbnailUrl))) {
      const images = asArray(video.thumbnailUrl).map((image) => resolveWithBase(ctx.meta.host, image));
      video.thumbnailUrl = images.length > 1 ? images : images[0];
    }
    if (video.thumbnail)
      video.thumbnail = resolveRelation(video.thumbnailUrl, ctx, imageResolver);
    return video;
  },
  resolveRootNode(video, { find }) {
    if (video.image && !video.thumbnail) {
      const firstImage = asArray(video.image)[0];
      setIfEmpty(video, "thumbnail", find(firstImage["@id"])?.url);
    }
  }
});

export { videoResolver };
