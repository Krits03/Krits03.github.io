import { logger } from "../../../util/logger.js";
import { defineTransformer } from "../../core/plugins.js";
export default defineTransformer([
  // need to make sure parent div has flex for the emoji to render inline
  {
    filter: (node) => node.type === "span" && node.props?.class?.includes("iconify"),
    transform: (node, e) => {
      if (import.meta.dev) {
        logger.warn(`When using the Nuxt Icon components in \`${e.options.component}\` you must provide \`mode="svg"\` to ensure correct rendering.`);
      }
    }
  },
  // need to make sure parent div has flex for the emoji to render inline
  {
    filter: (node) => node.type === "svg" && node.props?.class?.includes("iconify"),
    transform: (node) => {
      node.props.class = String(node.props.class).split(" ").filter((c) => !c.startsWith("iconify")).join(" ");
    }
  }
]);
