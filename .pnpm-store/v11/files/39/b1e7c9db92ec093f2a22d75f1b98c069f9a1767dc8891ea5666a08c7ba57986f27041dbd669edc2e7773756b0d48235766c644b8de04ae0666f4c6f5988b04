import { joinURL, encodeQueryItem } from "ufo";
import { createOperationsGenerator } from "../utils/index.js";
import { defineProvider } from "../utils/provider.js";
const operationsGenerator = createOperationsGenerator({
  keyMap: {
    width: "w",
    height: "h",
    dpr: "dpr",
    fit: "fit",
    gravity: "g",
    quality: "q",
    format: "f"
  },
  valueMap: {
    fit: {
      cover: "cover",
      contain: "contain",
      fill: "pad",
      outside: "crop",
      inside: "scale-down"
    },
    gravity: {
      auto: "auto",
      left: "left",
      right: "right",
      top: "top",
      bottom: "bottom",
      face: "face"
    },
    format: {
      auto: "auto",
      avif: "avif",
      webp: "webp",
      jpeg: "jpeg",
      png: "png",
      json: "json"
    }
  },
  joinWith: ",",
  formatter: (key, val) => encodeQueryItem(key, val)
});
export default defineProvider({
  getImage(imageId, { modifiers = {}, baseURL = "https://imagedelivery.net/", accountHash }) {
    const { variant, ...restModifiers } = modifiers;
    if (Object.keys(restModifiers).length === 0 || variant) {
      return {
        url: joinURL(baseURL, accountHash, imageId, variant ?? "public")
      };
    }
    const operations = operationsGenerator(restModifiers);
    return {
      url: joinURL(baseURL, accountHash, imageId, operations)
    };
  }
});
