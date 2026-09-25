import { joinURL, withQuery } from "ufo";
import { defineProvider } from "../utils/provider.js";
export const picsumCDN = "https://picsum.photos/";
export default defineProvider({
  getImage: (src, { modifiers, baseURL = picsumCDN }) => {
    const { width, height, grayscale, blur, ...otherModifiers } = modifiers || {};
    const parts = [];
    if (src && src !== "/") {
      const [type, id] = (src.startsWith("/") ? src.slice(1) : src).split("/");
      if (type && (type === "id" || type === "seed")) {
        parts.push(`${type}/${id}`);
      }
    }
    if (width) {
      parts.push(String(width));
    }
    if (height) {
      parts.push(String(height));
    }
    const query = {};
    if (grayscale) {
      query.grayscale = "";
    }
    if (blur !== void 0 && blur > 0) {
      query.blur = Math.min(Math.max(Math.round(blur), 1), 10);
    }
    for (const [key, value] of Object.entries(otherModifiers)) {
      if (value !== void 0 && value !== null && !["fit", "format", "quality", "background"].includes(key)) {
        query[key] = value;
      }
    }
    const url = joinURL(baseURL, ...parts);
    return {
      url: Object.keys(query).length > 0 ? withQuery(url, query) : url
    };
  }
});
