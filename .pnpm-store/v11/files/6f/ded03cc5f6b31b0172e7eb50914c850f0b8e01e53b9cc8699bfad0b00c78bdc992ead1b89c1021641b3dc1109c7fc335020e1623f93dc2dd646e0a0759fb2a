import { joinURL } from "ufo";
import { createOperationsGenerator } from "../utils/index.js";
import { defineProvider } from "../utils/provider.js";
const operationsGenerator = createOperationsGenerator({
  valueMap: {
    transforms(value) {
      return value.length > 0 ? JSON.stringify(
        Array.from(new Set(value.map((v) => JSON.stringify(v)))).map((v) => JSON.parse(v))
      ) : void 0;
    }
  }
});
function isKeyModifier(mod) {
  return !!mod && "key" in mod && typeof mod.key === "string";
}
export default defineProvider({
  getImage: (src, { modifiers, baseURL }) => {
    if (isKeyModifier(modifiers)) {
      return {
        url: joinURL(baseURL, src + `?key=${encodeURIComponent(modifiers.key)}`)
      };
    }
    const resolved = {
      ...modifiers,
      format: modifiers?.format === "jpeg" ? "jpg" : modifiers?.format
    };
    const operations = operationsGenerator(resolved);
    return {
      url: joinURL(baseURL, src + (operations ? `?${operations}` : ""))
    };
  }
});
