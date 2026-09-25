export const DEFAULT_XML_STREAM_CHUNK_SIZE = 64 * 1024;
export function isReadableStream(value) {
  return !!value && typeof value === "object" && typeof value.getReader === "function";
}
export function hasNonIdentityEncoding(value) {
  return (Array.isArray(value) ? value : [value]).flatMap((encoding) => String(encoding || "").split(",")).some((encoding) => encoding.trim().toLowerCase() !== "identity" && encoding.trim() !== "");
}
export function createNodeResponseStream(source, onCancelError) {
  const reader = source.getReader();
  const endListeners = /* @__PURE__ */ new Set();
  const errorListeners = /* @__PURE__ */ new Set();
  let aborted = false;
  let pumping = false;
  let releaseBackpressure;
  const stream = {
    abort(reason) {
      if (aborted)
        return;
      aborted = true;
      releaseBackpressure?.();
      releaseBackpressure = void 0;
      void reader.cancel(reason).catch(onCancelError);
    },
    on(event, listener) {
      if (event === "end")
        endListeners.add(listener);
      else
        errorListeners.add(listener);
      return stream;
    },
    pipe(destination) {
      if (pumping)
        return destination;
      pumping = true;
      void (async () => {
        try {
          while (true) {
            if (aborted)
              break;
            const result = await reader.read();
            if (result.done)
              break;
            if (!destination.write(result.value)) {
              await new Promise((resolve) => {
                releaseBackpressure = resolve;
                destination.once("drain", resolve);
              });
              releaseBackpressure = void 0;
            }
          }
          if (!aborted) {
            for (const listener of endListeners)
              listener();
          }
        } catch (error) {
          if (!aborted) {
            for (const listener of errorListeners)
              listener(error);
          }
        }
      })();
      return destination;
    }
  };
  return stream;
}
export function createChunkedXmlStream(chunks, targetChunkSize = DEFAULT_XML_STREAM_CHUNK_SIZE) {
  const iterator = chunks[Symbol.iterator]();
  const encoder = new TextEncoder();
  const chunkSize = Math.max(1, Math.floor(targetChunkSize));
  let complete = false;
  let pending;
  let pendingOffset = 0;
  return new ReadableStream({
    pull(controller) {
      if (complete)
        return;
      let output = "";
      while (output.length < chunkSize) {
        if (!pending) {
          const next = iterator.next();
          if (next.done) {
            complete = true;
            break;
          }
          pending = next.value;
          pendingOffset = 0;
          if (!pending)
            continue;
        }
        const remaining = chunkSize - output.length;
        let end = Math.min(pending.length, pendingOffset + remaining);
        if (end < pending.length && end > pendingOffset && pending.charCodeAt(end - 1) >= 55296 && pending.charCodeAt(end - 1) <= 56319) {
          end--;
          if (end === pendingOffset) {
            if (output)
              break;
            end = Math.min(pending.length, pendingOffset + 2);
          }
        }
        output += pending.slice(pendingOffset, end);
        pendingOffset = end;
        if (pendingOffset === pending.length)
          pending = void 0;
      }
      if (output)
        controller.enqueue(encoder.encode(output));
      if (complete)
        controller.close();
    },
    cancel() {
      complete = true;
      iterator.return?.();
    }
  });
}
export function negotiateCompressionEncoding(acceptEncoding) {
  if (!acceptEncoding.trim())
    return null;
  const explicit = /* @__PURE__ */ new Map();
  let wildcard;
  for (const value of acceptEncoding.split(",")) {
    const [rawEncoding, ...parameters] = value.trim().toLowerCase().split(";");
    if (!rawEncoding)
      continue;
    let quality = 1;
    for (const parameter of parameters) {
      const [key, rawValue] = parameter.trim().split("=");
      if (key === "q") {
        const parsed = Number.parseFloat(rawValue || "");
        quality = Number.isFinite(parsed) && parsed >= 0 && parsed <= 1 ? parsed : 0;
      }
    }
    if (rawEncoding === "*")
      wildcard = quality;
    else
      explicit.set(rawEncoding, quality);
  }
  const gzipQuality = explicit.get("gzip") ?? wildcard ?? 0;
  const deflateQuality = explicit.get("deflate") ?? wildcard ?? 0;
  if (gzipQuality <= 0 && deflateQuality <= 0)
    return null;
  return gzipQuality >= deflateQuality ? "gzip" : "deflate";
}
