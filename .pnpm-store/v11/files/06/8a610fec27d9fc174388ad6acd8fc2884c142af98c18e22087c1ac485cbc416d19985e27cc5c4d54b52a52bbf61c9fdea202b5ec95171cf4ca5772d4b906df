import { isNonFetchableLink } from "./inspections/util.js";
const responses = {};
const MockSuccessResponse = Promise.resolve({ status: 200, statusText: "OK", headers: {} });
export async function getLinkResponse({ link, timeout, fetchRemoteUrls, baseURL, isInStorage }) {
  if (link.includes("#") && !link.startsWith("#"))
    link = link.split("#")[0];
  link = decodeURI(link);
  if (link in responses) {
    return responses[link];
  }
  if (isNonFetchableLink(link)) {
    return null;
  }
  if (isInStorage()) {
    responses[link] = Promise.resolve({ status: 200, statusText: "OK", headers: { "X-Nuxt-Prerendered": true } });
    return responses[link];
  }
  if (link.startsWith("http") || link.startsWith("//")) {
    responses[link] = fetchRemoteUrls ? crawlFetch(link, { timeout, baseURL }) : MockSuccessResponse;
    return responses[link];
  }
  responses[link] = crawlFetch(link, { timeout, baseURL });
  return responses[link];
}
export function setLinkResponse(link, response) {
  responses[link] = response;
}
export async function getResolvedLinkResponses() {
  const data = {};
  for (const link in responses) {
    data[link] = await responses[link];
  }
  return data;
}
export async function crawlFetch(link, options = {}) {
  const timeout = options.timeout || 5e3;
  const timeoutController = new AbortController();
  const abortRequestTimeout = setTimeout(() => timeoutController.abort(), timeout);
  const start = Date.now();
  return await globalThis.$fetch.raw(encodeURI(link), {
    baseURL: options.baseURL,
    method: "HEAD",
    signal: timeoutController.signal,
    retry: 3,
    retryDelay: 250,
    headers: {
      "user-agent": "Nuxt Link Checker"
    }
  }).catch((error) => {
    if (error.name === "AbortError")
      return { status: 408, statusText: "Request Timeout", headers: {} };
    return { status: 404, statusText: "Not Found", headers: {} };
  }).finally(() => clearTimeout(abortRequestTimeout)).then((res) => {
    let headersObj = {};
    if (res.headers) {
      if (typeof res.headers.entries === "function") {
        headersObj = Object.fromEntries(Array.from(res.headers.entries()));
      } else if (typeof res.headers === "object") {
        headersObj = { ...res.headers };
      }
    }
    return { status: res.status, statusText: res.statusText, headers: headersObj, time: Date.now() - start };
  });
}
