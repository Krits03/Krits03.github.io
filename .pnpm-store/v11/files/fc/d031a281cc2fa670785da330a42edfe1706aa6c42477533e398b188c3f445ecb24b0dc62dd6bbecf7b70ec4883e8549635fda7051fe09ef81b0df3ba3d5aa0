import { createOperationsGenerator } from "../utils/index.js";
import { defineProvider } from "../utils/provider.js";
import { encodeQueryItem, joinURL } from "ufo";
import { defu } from "defu";
const operationsGenerator = createOperationsGenerator({
  keyMap: {
    width: "width",
    height: "height",
    focalPointXY: "rxy",
    format: "format",
    quality: "quality",
    fit: "rmode",
    sampler: "rsampler",
    anchorPosition: "ranchor"
  },
  joinWith: "&",
  formatter: (key, value) => encodeQueryItem(key, value)
});
const defaultModifiers = {};
export default defineProvider({
  getImage: (src, {
    modifiers: _modifiers,
    baseURL = ""
  }) => {
    const modifiers = { ..._modifiers };
    if (modifiers.fit === "contain") {
      modifiers.fit = "max";
    } else if (modifiers.fit === "cover") {
      modifiers.fit = "crop";
    }
    const mergedModifiers = defu(modifiers, defaultModifiers);
    const operations = operationsGenerator(mergedModifiers);
    return {
      url: joinURL(baseURL, src + (operations ? "?" + operations : ""))
    };
  }
});
