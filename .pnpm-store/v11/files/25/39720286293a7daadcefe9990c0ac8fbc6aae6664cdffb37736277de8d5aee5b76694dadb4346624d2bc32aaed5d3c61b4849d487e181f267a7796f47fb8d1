import { r as readInput } from './shared/sitemapd.CGXN3Oad.mjs';

async function cancelResponseBody(body, reason) {
  if (!body)
    return;
  await body.cancel(reason).catch(() => {
  });
}
function createFetchDocumentLoader(options) {
  return async (request) => {
    let response;
    try {
      response = await options.fetch(request.url, {
        method: "GET",
        redirect: "manual",
        ...options.headers ? { headers: options.headers } : {},
        ...request.signal ? { signal: request.signal } : {}
      });
    } catch (error) {
      const name = error instanceof DOMException || error instanceof Error ? error.name : "";
      return {
        _tag: "load_error",
        url: request.url,
        code: name === "TimeoutError" ? "timeout" : name === "AbortError" ? "cancelled" : "network",
        detail: error instanceof Error ? error.message : String(error)
      };
    }
    if (response.status >= 300 && response.status < 400) {
      const location = response.headers.get("location");
      if (!location) {
        await cancelResponseBody(response.body, "redirect response rejected");
        return {
          _tag: "http_error",
          url: request.url,
          status: response.status,
          statusText: "Redirect response is missing Location"
        };
      }
      let resolved;
      try {
        resolved = new URL(location, request.url).toString();
      } catch {
        await cancelResponseBody(response.body, "invalid redirect response rejected");
        return {
          _tag: "http_error",
          url: request.url,
          status: response.status,
          statusText: "Redirect response has an invalid Location"
        };
      }
      await cancelResponseBody(response.body, "redirect followed manually");
      return {
        _tag: "redirect",
        url: request.url,
        location: resolved,
        status: response.status
      };
    }
    if (response.status === 404 || response.status === 410) {
      await cancelResponseBody(response.body, "not found response body is unused");
      return { _tag: "not_found", url: request.url, status: response.status };
    }
    if (!response.ok) {
      await cancelResponseBody(response.body, "error response body is unused");
      return {
        _tag: "http_error",
        url: request.url,
        status: response.status,
        statusText: response.statusText
      };
    }
    if (!response.body) {
      return {
        _tag: "body",
        url: request.url,
        body: new Uint8Array()
      };
    }
    if (request.maxWireBytes !== void 0) {
      const read = await readInput(response.body, request.maxWireBytes);
      if (read._tag === "limit") {
        return {
          _tag: "load_error",
          url: request.url,
          code: "wire_limit",
          detail: `Sitemap response exceeds ${request.maxWireBytes} wire bytes`,
          bytesRead: read.bytesRead
        };
      }
      return {
        _tag: "body",
        url: request.url,
        body: read.chunks
      };
    }
    return {
      _tag: "body",
      url: request.url,
      body: response.body
    };
  };
}

export { createFetchDocumentLoader };
