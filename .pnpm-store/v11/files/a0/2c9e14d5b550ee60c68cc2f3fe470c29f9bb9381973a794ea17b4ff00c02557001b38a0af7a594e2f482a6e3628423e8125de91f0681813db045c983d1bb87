import { removeResponseHeader } from "#nuxtseo/h3";
import { defineNitroPlugin } from "#nuxtseo/nitro";
import { logger } from "../../utils-pure.js";
import { createNodeResponseStream, isReadableStream } from "../sitemap/stream.js";
export default defineNitroPlugin((nitro) => {
  nitro.hooks.hook("beforeResponse", (event, response) => {
    const nodeResponse = event.node.res;
    if (!event.context._isSitemap || !isReadableStream(response.body) || !nodeResponse?.socket || typeof nodeResponse?.write !== "function" || typeof nodeResponse?.once !== "function") {
      return;
    }
    response.body = createNodeResponseStream(response.body, (error) => {
      logger.error("Failed to cancel sitemap response stream after the client disconnected.", error);
    });
    removeResponseHeader(event, "Content-Length");
  });
});
