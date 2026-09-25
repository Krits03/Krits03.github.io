import { serverQueryContent } from "#content/server";
import { defineEventHandler } from "#nuxtseo/h3";
export default defineEventHandler(async (e) => {
  const contentList = await serverQueryContent(e).find();
  return contentList.map((c) => c.sitemap).filter(Boolean);
});
