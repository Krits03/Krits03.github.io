import { createHead, renderSSRHead } from "@unhead/vue/server";
import { createError } from "#nuxtseo/h3";
import resolvedFonts from "#og-image/fonts";
import { fetchIsland } from "../../util/kit.js";
import { applyEmojis } from "../core/transforms/emojis/index.js";
const RE_SCRIPT_TAG = /<script\b[^<]*(?:(?!<\/script>)<[^<]*)*<\/script>/gi;
export async function html(ctx) {
  const { options } = ctx;
  const fonts = resolvedFonts;
  if (!options.component) {
    throw createError({
      statusCode: 500,
      statusMessage: `[Nuxt OG Image] Rendering an invalid component. Received options: ${JSON.stringify(options)}.`
    });
  }
  const islandTimeout = ctx.runtimeConfig.security?.renderTimeout ?? 15e3;
  const island = await fetchIsland(ctx.e, ctx.options.component, typeof ctx.options.props !== "undefined" ? ctx.options.props : ctx.options, islandTimeout);
  const head = createHead();
  head.push(island.head);
  let defaultFontFamily = "sans-serif";
  const firstFont = fonts[0];
  if (firstFont)
    defaultFontFamily = firstFont.family.replaceAll("+", " ");
  await applyEmojis(ctx, island);
  let html2 = island.html;
  const scale = options.props?.scale || 1;
  const scaledWidth = Math.round(Number(options.width) * scale);
  const scaledHeight = Math.round(Number(options.height) * scale);
  const fontFaces = fonts.map((font) => {
    const ext = font.src.split(".").pop()?.toLowerCase();
    const format = ext === "woff2" ? "woff2" : ext === "woff" ? "woff" : "truetype";
    return `@font-face {
  font-family: '${font.family.replaceAll("+", " ")}';
  font-style: ${font.style};
  font-weight: ${font.weight};
  src: url('${font.src}') format('${format}');
}`;
  }).join("\n");
  const bgColor = options.props?.colorMode === "dark" ? "#1b1b1b" : "#fff";
  head.push({
    style: [
      {
        innerHTML: `/* reset */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
img, svg { display: block; max-width: 100%; }

/* viewport */
html, body {
  width: ${scaledWidth}px;
  height: ${scaledHeight}px;
  overflow: hidden;
  font-family: '${defaultFontFamily}', sans-serif;
  background-color: ${bgColor};
}

/* scale wrapper */
.og-scale-wrapper {
  transform: scale(${scale});
  transform-origin: top left;
  width: ${options.width}px;
  height: ${options.height}px;
}
.og-scale-wrapper > :first-child {
  width: 100%;
  height: 100%;
}

/* match satori flex defaults for divs */
div { display: flex; }
div:has(div, p, ul, ol, li, blockquote, pre, hr, table, dl) {
  flex-direction: column;
}
div:not(:has(div, p, ul, ol, li, blockquote, pre, hr, table, dl)) {
  flex-wrap: wrap;
  gap: 12px;
}

svg[data-emoji] { display: inline-block; }

/* fonts */
${fontFaces}`
      }
    ],
    meta: [
      { charset: "utf-8" }
    ]
  });
  RE_SCRIPT_TAG.lastIndex = 0;
  html2 = html2.replaceAll(RE_SCRIPT_TAG, "");
  const headChunk = await renderSSRHead(head);
  return `<!DOCTYPE html>
<html ${headChunk.htmlAttrs}>
<head>${headChunk.headTags}</head>
<body ${headChunk.bodyAttrs}>${headChunk.bodyTagsOpen}<div class="og-scale-wrapper" data-v-inspector-ignore="true">${html2}</div>${headChunk.bodyTags}</body>
</html>`;
}
