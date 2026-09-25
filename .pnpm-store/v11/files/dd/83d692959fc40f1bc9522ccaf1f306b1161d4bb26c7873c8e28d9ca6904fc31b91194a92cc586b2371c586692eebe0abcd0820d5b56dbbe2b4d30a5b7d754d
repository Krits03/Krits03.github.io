import { collectSitemap } from "sitemapd/parse";
import { defineEventHandler, getQuery } from "#nuxtseo/h3";
async function fetchSitemapBody(url) {
  const response = await fetch(url, {
    headers: { Accept: "application/xml, text/xml, application/gzip" },
    signal: AbortSignal.timeout(15e3)
  });
  if (!response.ok)
    throw new Error(`HTTP ${response.status}: ${response.statusText}`);
  return new Uint8Array(await response.arrayBuffer());
}
export default defineEventHandler(async (e) => {
  const { url, mode } = getQuery(e);
  if (!url || typeof url !== "string")
    return { url: "", isIndex: false, sitemaps: [], warnings: [], error: "Missing url query parameter" };
  if (mode === "debug") {
    const debugUrl = `${url.replace(/\/$/, "")}/__sitemap__/debug.json`;
    const response = await fetch(debugUrl, {
      headers: { Accept: "application/json" },
      signal: AbortSignal.timeout(1e4)
    }).catch(() => {
      return null;
    });
    if (response?.ok) {
      const json = await response.json().catch(() => {
        return null;
      });
      if (json?.sitemaps)
        return json;
    }
  }
  const sitemapUrl = url.endsWith("/") ? `${url}sitemap.xml` : url;
  const body = await fetchSitemapBody(sitemapUrl).catch((err) => {
    return err;
  });
  if (body instanceof Error)
    return { url: sitemapUrl, isIndex: false, sitemaps: [], warnings: [], error: `Failed to fetch sitemap: ${body.message}` };
  const parsed = await collectSitemap(body);
  if (parsed._tag !== "document") {
    return {
      url: sitemapUrl,
      isIndex: false,
      sitemaps: [],
      warnings: parsed.issues,
      error: parsed.issues.map((issue) => issue.message).join("; ") || "Invalid sitemap document"
    };
  }
  if (parsed.document._tag === "index") {
    const { entries } = parsed.document;
    const sitemaps = await Promise.all(
      entries.map(async (entry) => {
        const childBody = await fetchSitemapBody(entry.loc).catch((err) => err);
        if (childBody instanceof Error) {
          return {
            loc: entry.loc,
            urlCount: 0,
            warnings: [],
            error: childBody.message,
            lastmod: entry.lastmod
          };
        }
        const result = await collectSitemap(childBody);
        if (result._tag !== "document" || result.document._tag !== "urlset") {
          return {
            loc: entry.loc,
            urlCount: 0,
            warnings: result.issues,
            error: result.issues.map((issue) => issue.message).join("; ") || "Child is not a URL set",
            lastmod: entry.lastmod
          };
        }
        return {
          loc: entry.loc,
          urlCount: result.document.entries.length,
          warnings: result.issues,
          lastmod: entry.lastmod
        };
      })
    );
    return { url: sitemapUrl, isIndex: true, sitemaps, warnings: parsed.issues };
  }
  return {
    url: sitemapUrl,
    isIndex: false,
    sitemaps: [{
      loc: sitemapUrl,
      urlCount: parsed.document.entries.length,
      warnings: parsed.issues
    }],
    warnings: []
  };
});
