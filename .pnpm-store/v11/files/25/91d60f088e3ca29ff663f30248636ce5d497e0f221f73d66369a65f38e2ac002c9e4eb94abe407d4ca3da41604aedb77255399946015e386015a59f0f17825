import { appendResponseHeader, getRequestHeader, getResponseHeader, removeResponseHeader, setResponseHeader } from "#nuxtseo/h3";
import { defineNitroPlugin } from "#nuxtseo/nitro";
import { logger } from "../../utils-pure.js";
import { hasNonIdentityEncoding, isReadableStream, negotiateCompressionEncoding } from "../sitemap/stream.js";
let warnedAboutCompressionStream = false;
const NODE_COMPRESSION_INPUT_BATCH_BYTES = 512 * 1024;
function toByteStream(body) {
  if (isReadableStream(body))
    return body;
  if (body instanceof Blob)
    return body.stream();
  const value = typeof body === "string" || body instanceof ArrayBuffer || ArrayBuffer.isView(body) ? body : JSON.stringify(body);
  return new Blob([value]).stream();
}
function createNodeCompressionInputStream(source) {
  const reader = source.getReader();
  let bytesRead = 0;
  return new ReadableStream({
    async pull(controller) {
      if (bytesRead >= NODE_COMPRESSION_INPUT_BATCH_BYTES) {
        bytesRead = 0;
        await new Promise((resolve) => setTimeout(resolve, 0));
      }
      const result = await reader.read();
      if (result.done) {
        controller.close();
        return;
      }
      bytesRead += result.value.byteLength;
      controller.enqueue(result.value);
    },
    cancel(reason) {
      return reader.cancel(reason);
    }
  });
}
function addVaryAcceptEncoding(event) {
  const vary = getResponseHeader(event, "Vary");
  const values = (Array.isArray(vary) ? vary : [vary]).flatMap((value) => String(value || "").split(",")).map((value) => value.trim().toLowerCase());
  if (!values.includes("*") && !values.includes("accept-encoding"))
    appendResponseHeader(event, "Vary", "Accept-Encoding");
}
export default defineNitroPlugin((nitro) => {
  nitro.hooks.hook("beforeResponse", (event, response) => {
    if (!event.context._isSitemap || !response.body)
      return;
    addVaryAcceptEncoding(event);
    if (hasNonIdentityEncoding(getResponseHeader(event, "Content-Encoding")))
      return;
    const encoding = negotiateCompressionEncoding(getRequestHeader(event, "accept-encoding") || "");
    if (!encoding)
      return;
    if (typeof CompressionStream === "undefined") {
      if (!warnedAboutCompressionStream) {
        warnedAboutCompressionStream = true;
        logger.warn("Sitemap compression was requested, but CompressionStream is unavailable in this runtime. Sending the uncompressed response.");
      }
      return;
    }
    const compression = new CompressionStream(encoding);
    const source = toByteStream(response.body);
    const compressionInput = event.node.res?.socket ? createNodeCompressionInputStream(source) : source;
    response.body = compressionInput.pipeThrough(compression);
    removeResponseHeader(event, "Content-Length");
    setResponseHeader(event, "Content-Encoding", encoding);
  });
});
