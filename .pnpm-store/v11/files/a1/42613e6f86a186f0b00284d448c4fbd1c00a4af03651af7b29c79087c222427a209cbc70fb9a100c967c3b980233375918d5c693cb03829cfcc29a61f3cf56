import { joinURL } from "ufo";
import { defineProvider } from "../utils/provider.js";
const fitMap = {
  contain: "",
  cover: "r",
  fill: "!",
  inside: "",
  outside: "r"
};
function encodeColor(color) {
  const hex = color.startsWith("#") ? color.slice(1) : color;
  if (typeof globalThis.btoa === "function") {
    return globalThis.btoa(hex).replace(/\+/g, "-").replace(/\//g, "_").replace(/=+$/, "");
  }
  return Buffer.from(hex).toString("base64").replace(/\+/g, "-").replace(/\//g, "_").replace(/=+$/, "");
}
export default defineProvider({
  getImage: (src, { modifiers = {}, baseURL }) => {
    if (!baseURL) {
      throw new Error("EdgeOne Pages provider requires baseURL to be set");
    }
    const {
      width,
      height,
      fit,
      quality,
      format,
      background,
      blur,
      crop,
      gravity,
      dx,
      dy,
      iradius,
      scrop,
      rotate,
      autoOrient,
      sharpen,
      strip,
      interlace,
      pad
    } = modifiers;
    const operations = [];
    if (width || height) {
      const w = width ?? "";
      const h = height ?? "";
      const fitSuffix = fit ? fitMap[fit] ?? "" : "";
      if (fitSuffix === "r") {
        operations.push(`thumbnail/!${w}x${h}r`);
      } else if (fitSuffix === "!") {
        operations.push(`thumbnail/${w}x${h}!`);
      } else {
        operations.push(`thumbnail/${w}x${h}`);
      }
    }
    if (pad || background && (width || height)) {
      operations.push("pad/1");
      if (background) {
        operations.push(`color/${encodeColor(background)}`);
      }
    }
    if (crop) {
      operations.push(`crop/${crop}`);
      if (gravity) {
        operations.push(`gravity/${gravity}`);
      }
      if (typeof dx !== "undefined") {
        operations.push(`dx/${dx}`);
      }
      if (typeof dy !== "undefined") {
        operations.push(`dy/${dy}`);
      }
    }
    if (typeof iradius !== "undefined") {
      operations.push(`iradius/${iradius}`);
    }
    if (scrop) {
      operations.push(`scrop/${scrop}`);
    }
    if (typeof rotate !== "undefined") {
      operations.push(`rotate/${rotate}`);
    }
    if (autoOrient) {
      operations.push("auto-orient");
    }
    if (typeof quality !== "undefined") {
      operations.push(`quality/${quality}`);
    }
    if (format) {
      const mappedFormat = format === "jpeg" ? "jpg" : format;
      operations.push(`format/${mappedFormat}`);
    }
    if (typeof blur !== "undefined" && blur) {
      operations.push(`blur/${blur}x${blur}`);
    }
    if (typeof sharpen !== "undefined") {
      operations.push(`sharpen/${sharpen}`);
    }
    if (strip) {
      operations.push("strip");
    }
    if (interlace) {
      operations.push(`interlace/${typeof interlace === "number" ? interlace : 1}`);
    }
    const query = operations.length ? `?imageMogr2/${operations.join("/")}` : "";
    return {
      url: joinURL(baseURL, src + query)
    };
  }
});
