export function extractRobotsMetaFromHtml(html) {
  const metaTag = html.match(/<meta\s[^>]*\bname=["']robots["'][^>]*>/i)?.[0];
  if (!metaTag)
    return null;
  const content = metaTag.match(/(?:^|\s)content=["']([^"']+)["']/i)?.[1] || null;
  const productionContent = metaTag.match(/(?:^|\s)data-production-content=["']([^"']+)["']/i)?.[1] || null;
  const hint = metaTag.match(/(?:^|\s)data-hint=["']([^"']+)["']/i)?.[1] || null;
  return { content, productionContent, hint };
}
