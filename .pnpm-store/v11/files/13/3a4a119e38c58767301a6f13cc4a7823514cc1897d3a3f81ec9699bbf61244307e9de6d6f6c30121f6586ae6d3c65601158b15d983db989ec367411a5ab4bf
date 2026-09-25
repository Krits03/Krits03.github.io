import { joinURL, withLeadingSlash } from "ufo";
import { defineNitroPlugin } from "#nuxtseo/nitro";
import { useSitemapRuntimeConfig } from "../utils.js";
export default defineNitroPlugin((nitroApp) => {
  const { sitemaps, sitemapsPathPrefix } = useSitemapRuntimeConfig();
  const queue = [];
  const timeoutIds = [];
  const enqueue = (path) => {
    queue.push(() => nitroApp.localFetch(withLeadingSlash(path), {}));
  };
  for (const [name, sitemap] of Object.entries(sitemaps)) {
    if (!sitemap._route)
      continue;
    if (name === "index") {
      enqueue(sitemap._route);
      continue;
    }
    const def = sitemap;
    if (def.chunks || def._isChunking) {
      enqueue(joinURL(sitemapsPathPrefix || "/", `${name}-0.xml`));
    } else {
      enqueue(sitemap._route);
    }
  }
  const initialTimeout = setTimeout(
    () => {
      const next = async () => {
        if (queue.length === 0) {
          timeoutIds.length = 0;
          return;
        }
        try {
          await queue.shift()();
        } catch (error) {
          console.error("[sitemap:warm-up] Error warming up sitemap:", error);
        }
        if (queue.length > 0) {
          const nextTimeout = setTimeout(next, 1e3);
          timeoutIds.push(nextTimeout);
        }
      };
      next();
    },
    2500
    /* https://github.com/unjs/nitro/pull/1906 */
  );
  timeoutIds.push(initialTimeout);
  nitroApp.hooks.hook("close", () => {
    timeoutIds.forEach((id) => clearTimeout(id));
    timeoutIds.length = 0;
    queue.length = 0;
  });
});
