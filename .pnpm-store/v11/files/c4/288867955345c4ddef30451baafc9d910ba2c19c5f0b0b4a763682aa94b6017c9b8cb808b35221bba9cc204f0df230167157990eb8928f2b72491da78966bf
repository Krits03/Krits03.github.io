import { decodeHtml } from "../../../util/encoding.js";
import { defineTransformer } from "../plugins.js";
export default defineTransformer([
  // clean up vue inspector data attributes
  {
    filter: (node) => node.props?.["data-v-inspector"],
    transform: (node) => {
      delete node.props["data-v-inspector"];
    }
  },
  // decode HTML entities in string children
  {
    filter: (node) => typeof node.props?.children === "string",
    transform: (node) => {
      node.props.children = decodeHtml(node.props.children);
    }
  },
  // decode HTML entities in array children (text nodes with siblings)
  {
    filter: (node) => Array.isArray(node.props?.children),
    transform: (node) => {
      node.props.children = node.props.children.map(
        (child) => typeof child === "string" ? decodeHtml(child) : child
      );
    }
  }
]);
