function inputFailure(reason, message) {
  return Object.assign(new Error(message), {
    _tag: "sitemap_input_failure",
    reason
  });
}
function isSitemapInputFailure(error) {
  return Boolean(
    error && typeof error === "object" && "_tag" in error && error._tag === "sitemap_input_failure"
  );
}
function isReadableStream(input) {
  return typeof input === "object" && input !== null && "getReader" in input && typeof input.getReader === "function";
}
function isAsyncIterable(input) {
  return typeof input === "object" && input !== null && Symbol.asyncIterator in input;
}
function isIterable(input) {
  return typeof input === "object" && input !== null && Symbol.iterator in input;
}
async function* streamChunks(stream) {
  const reader = stream.getReader();
  let done = false;
  try {
    while (!done) {
      const next = await reader.read();
      done = next.done;
      if (next.value !== void 0)
        yield next.value;
    }
  } finally {
    if (!done)
      await reader.cancel("sitemap input stopped before completion");
    reader.releaseLock();
  }
}
async function* chunks(input) {
  if (typeof input === "string" || input instanceof Uint8Array) {
    yield input;
    return;
  }
  if (isReadableStream(input)) {
    yield* streamChunks(input);
    return;
  }
  if (isAsyncIterable(input)) {
    yield* input;
    return;
  }
  if (isIterable(input))
    yield* input;
}
async function* byteChunks(input) {
  const encoder = new TextEncoder();
  for await (const chunk of chunks(input))
    yield typeof chunk === "string" ? encoder.encode(chunk) : chunk;
}
async function* replayBytes(initial, iterator) {
  let done = false;
  try {
    yield* initial;
    while (!done) {
      const next = await iterator.next();
      done = Boolean(next.done);
      if (next.value)
        yield next.value;
    }
  } finally {
    if (!done)
      await iterator.return?.();
  }
}
function iteratorStream(iterator) {
  return new ReadableStream({
    async pull(controller) {
      const next = await iterator.next();
      if (next.done) {
        controller.close();
        return;
      }
      if (next.value)
        controller.enqueue(next.value);
    },
    async cancel() {
      await iterator.return?.();
    }
  });
}
function gzipPrefix(chunks2) {
  const first = chunks2.flatMap((chunk) => [...chunk.subarray(0, 2)]);
  return first.length >= 2 && first[0] === 31 && first[1] === 139;
}
function utf8ByteLength(input) {
  let bytes = 0;
  for (let index = 0; index < input.length; index++) {
    const code = input.charCodeAt(index);
    if (code <= 127) {
      bytes++;
    } else if (code <= 2047) {
      bytes += 2;
    } else if (code >= 55296 && code <= 56319) {
      const next = input.charCodeAt(index + 1);
      if (next < 56320 || next > 57343)
        return void 0;
      bytes += 4;
      index++;
    } else if (code >= 56320 && code <= 57343) {
      return void 0;
    } else {
      bytes += 3;
    }
  }
  return bytes;
}
async function* decodedTextChunks(input, maxDecodedBytes, stats) {
  if (typeof input === "string") {
    const bytes = utf8ByteLength(input);
    if (bytes !== void 0) {
      stats.bytesRead = bytes;
      if (bytes > maxDecodedBytes) {
        throw inputFailure(
          "decoded_limit",
          `Sitemap exceeds ${maxDecodedBytes} decoded bytes`
        );
      }
      if (input)
        yield input;
      return;
    }
  }
  const iterator = byteChunks(input)[Symbol.asyncIterator]();
  const initial = [];
  let prefixBytes = 0;
  while (prefixBytes < 2) {
    const next = await iterator.next();
    if (next.done)
      break;
    if (next.value) {
      initial.push(next.value);
      prefixBytes += next.value.byteLength;
    }
  }
  stats.compressed = gzipPrefix(initial);
  const replay = replayBytes(initial, iterator);
  const decodedBytes = stats.compressed ? streamChunks(
    iteratorStream(replay[Symbol.asyncIterator]()).pipeThrough(
      new DecompressionStream("gzip")
    )
  ) : replay;
  const decoder = new TextDecoder("utf-8", { fatal: true });
  try {
    for await (const bytes of decodedBytes) {
      stats.bytesRead += bytes.byteLength;
      if (stats.bytesRead > maxDecodedBytes) {
        throw inputFailure(
          "decoded_limit",
          `Sitemap exceeds ${maxDecodedBytes} decoded bytes`
        );
      }
      let text;
      try {
        text = decoder.decode(bytes, { stream: true });
      } catch {
        throw inputFailure("invalid_utf8", "Sitemap contains invalid UTF-8");
      }
      if (text)
        yield text;
    }
    const tail = decoder.decode();
    if (tail)
      yield tail;
  } catch (error) {
    if (isSitemapInputFailure(error) || !stats.compressed)
      throw error;
    throw inputFailure(
      "malformed",
      error instanceof Error ? error.message : "Invalid gzip sitemap body"
    );
  }
}
async function readInput(input, maxBytes) {
  const collected = [];
  let bytesRead = 0;
  for await (const bytes of byteChunks(input)) {
    bytesRead += bytes.byteLength;
    if (bytesRead > maxBytes)
      return { _tag: "limit", bytesRead };
    collected.push(bytes);
  }
  return { _tag: "success", chunks: collected, bytesRead };
}

export { decodedTextChunks as d, isSitemapInputFailure as i, readInput as r };
