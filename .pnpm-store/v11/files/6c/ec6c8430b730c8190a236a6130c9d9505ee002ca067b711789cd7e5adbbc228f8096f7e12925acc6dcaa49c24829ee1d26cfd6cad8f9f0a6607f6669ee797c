import { useNitroApp } from "#nuxtseo/nitro";
import { getEmojiCodePoint, getEmojiIconNames } from "./emoji-utils.js";
function wrapDefsElements(body) {
  const defsElements = ["linearGradient", "radialGradient", "filter", "clipPath", "mask", "pattern"];
  const defsRegex = new RegExp(`<(${defsElements.join("|")})[\\s\\S]*?<\\/\\1>`, "g");
  if (body.includes("<defs>") || body.includes("<defs ")) {
    return body;
  }
  const foundDefs = [];
  const result = body.replace(defsRegex, (match) => {
    foundDefs.push(match);
    return "";
  });
  if (foundDefs.length > 0) {
    return `<defs>${foundDefs.join("")}</defs>${result}`;
  }
  return body;
}
export async function getEmojiSvg(ctx, emojiChar) {
  const nitroApp = useNitroApp();
  if (!nitroApp._ogImageIconsData) {
    const { loadIcons } = await import("#og-image-virtual/iconify-json-icons.mjs");
    nitroApp._ogImageIconsData = await loadIcons();
  }
  const { icons, width: pkgWidth, height: pkgHeight } = nitroApp._ogImageIconsData;
  const codePoint = getEmojiCodePoint(emojiChar);
  const possibleNames = getEmojiIconNames(codePoint, ctx.options.emojis);
  for (const iconName of possibleNames) {
    if (icons[iconName]) {
      const iconData = icons[iconName];
      const body = wrapDefsElements(iconData.body || "");
      const width = iconData.width || pkgWidth || 128;
      const height = iconData.height || pkgHeight || 128;
      return `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 ${width} ${height}" width="1em" height="1em" style="display:inline-block;vertical-align:middle">${body}</svg>`;
    }
  }
  return null;
}
