import { joinURL, hasProtocol } from "ufo";
import { createOperationsGenerator } from "../utils/index.js";
import { defineProvider } from "../utils/provider.js";
const operationsGenerator = createOperationsGenerator({
  keyMap: {
    // Core dimensions
    width: "w",
    height: "h",
    quality: "q",
    format: "o",
    rotate: "r",
    // Cropping
    crop: "c",
    gravity: "g",
    // WebP
    webpLossless: "webpl",
    webpMethod: "webpm",
    // JPEG XL
    jxlEffort: "jxlef",
    jxlDecodingSpeed: "jxlds",
    // Cache
    refresh: "rf",
    version: "v",
    // Text / Watermark
    text: "t",
    textColor: "tc",
    textSize: "ts",
    textBackground: "tbg",
    // Image Processing
    background: "bg",
    strip: "st",
    autoOrient: "ao",
    resize: "rz",
    mozjpeg: "moz",
    unsharp: "unsh",
    sharpen: "sh",
    blur: "blr",
    filter: "f",
    scale: "sc",
    samplingFactor: "sf",
    preserveAspectRatio: "par",
    preserveNaturalSize: "pns",
    // Advanced
    faceCrop: "fc",
    faceCropPosition: "fcp",
    faceBlur: "fb",
    smartCrop: "smc",
    colorspace: "clsp",
    monochrome: "mnchr",
    // PDF
    pdfPage: "pdfp",
    density: "dnst",
    // Video
    videoTime: "tm",
    // Extract
    extract: "e",
    extractTopX: "p1x",
    extractTopY: "p1y",
    extractBottomX: "p2x",
    extractBottomY: "p2y",
    // Other
    extent: "ett",
    gifFrame: "gf"
  },
  valueMap: {
    // Booleans become 0 / 1
    crop: Number,
    webpLossless: Number,
    refresh: Number,
    autoOrient: Number,
    resize: Number,
    scale: Number,
    faceCrop: Number,
    faceBlur: Number,
    smartCrop: Number,
    monochrome: Number,
    extract: Number,
    // Inverted-defaults (strip/mozjpeg/par/pns default ON on the server;
    // we only emit them when explicitly set to false — see getImage pre-processing)
    strip: Number,
    mozjpeg: Number,
    preserveAspectRatio: Number,
    preserveNaturalSize: Number,
    // Encode # so it does not break the URL path segment
    background: (value) => value.replaceAll("#", "%23"),
    textColor: (value) => value.replaceAll("#", "%23"),
    textBackground: (value) => value.replaceAll("#", "%23"),
    // Encode text watermarks
    text: (value) => encodeURIComponent(value)
  },
  joinWith: ",",
  formatter: (key, value) => `${key}_${value}`
});
export default defineProvider({
  getImage: (src, options) => {
    const {
      modifiers: rawModifiers = {},
      baseURL,
      sourceURL,
      processType = "upload"
    } = options;
    if (import.meta.dev && !baseURL) {
      console.warn("[nuxt] [image] [flyimg] `baseURL` is required. Set it in your nuxt.config under `image.flyimg.baseURL`.");
    }
    const {
      fit,
      strip,
      mozjpeg,
      preserveAspectRatio,
      preserveNaturalSize,
      ...rest
    } = rawModifiers;
    const modifiers = { ...rest };
    switch (fit) {
      case "cover":
        if (!modifiers.crop) modifiers.crop = true;
        break;
      case "fill":
        if (preserveAspectRatio !== false) modifiers.preserveAspectRatio = false;
        break;
      case "contain":
      case "inside":
        break;
      case "outside":
        if (import.meta.dev) {
          console.warn('[nuxt] [image] [flyimg] fit="outside" is not supported by Flyimg and will be ignored.');
        }
        break;
    }
    const isDisabled = (v) => v === false || v === 0 || v === "0";
    if (strip != null && isDisabled(strip)) modifiers.strip = false;
    if (mozjpeg != null && isDisabled(mozjpeg)) modifiers.mozjpeg = false;
    if (preserveAspectRatio != null && isDisabled(preserveAspectRatio)) modifiers.preserveAspectRatio = false;
    if (preserveNaturalSize != null && isDisabled(preserveNaturalSize)) modifiers.preserveNaturalSize = false;
    if (import.meta.dev && !hasProtocol(src) && !sourceURL) {
      console.warn("[nuxt] [image] [flyimg] `src` is a relative path but `sourceURL` is not configured. Flyimg requires an absolute source URL. Set `image.flyimg.sourceURL` in your nuxt.config.");
    }
    const imageUrl = !hasProtocol(src) && sourceURL ? joinURL(sourceURL, src) : src;
    const operations = operationsGenerator(modifiers);
    const imageOptions = operations || "-";
    return {
      url: joinURL(baseURL || "/", `${processType}/${imageOptions}/${imageUrl}`)
    };
  }
});
