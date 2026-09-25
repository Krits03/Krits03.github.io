import { getEmojiSvg } from "#og-image/emoji-transform";
import { RE_MATCH_EMOJIS } from "./emoji-utils.js";
const RE_SVG_ID_ATTR = /\bid="([^"]+)"/g;
const RE_HTML_TEXT_CONTENT = />([^<]*)</g;
const RE_REGEX_SPECIAL_CHARS = /[.*+?^${}()|[\]\\]/g;
let emojiCounter = 0;
function wrapDefsElements(svg) {
  const defsElements = ["linearGradient", "radialGradient", "filter", "clipPath", "mask", "pattern"];
  const defsRegex = new RegExp(`<(${defsElements.join("|")})[\\s\\S]*?<\\/\\1>`, "g");
  if (svg.includes("<defs>") || svg.includes("<defs ")) {
    return svg;
  }
  const foundDefs = [];
  let result = svg.replace(defsRegex, (match) => {
    foundDefs.push(match);
    return "";
  });
  if (foundDefs.length > 0) {
    const svgTagEnd = result.indexOf(">") + 1;
    result = `${result.slice(0, svgTagEnd)}<defs>${foundDefs.join("")}</defs>${result.slice(svgTagEnd)}`;
  }
  return result;
}
function makeIdsUnique(svg) {
  const prefix = `e${emojiCounter++}_`;
  const ids = /* @__PURE__ */ new Set();
  svg.replace(RE_SVG_ID_ATTR, (_, id) => {
    ids.add(id);
    return "";
  });
  let result = svg;
  for (const id of ids) {
    result = result.replace(new RegExp(`id="${id}"`, "g"), `id="${prefix}${id}"`).replace(new RegExp(`url\\(#${id}\\)`, "g"), `url(#${prefix}${id})`).replace(new RegExp(`href="#${id}"`, "g"), `href="#${prefix}${id}"`);
  }
  return result;
}
export async function applyEmojis(ctx, island) {
  if (!island.html || !ctx.options.emojis)
    return;
  const matches = [...island.html.matchAll(RE_MATCH_EMOJIS)];
  if (!matches.length)
    return;
  const emojiToSvg = /* @__PURE__ */ new Map();
  const uniqueEmojis = [...new Set(matches.map((m) => m[0]))];
  await Promise.all(uniqueEmojis.map(async (emoji) => {
    let svg = await getEmojiSvg(ctx, emoji);
    if (svg) {
      svg = makeIdsUnique(svg);
      svg = wrapDefsElements(svg);
    }
    emojiToSvg.set(emoji, svg ?? null);
  }));
  let html = island.html;
  html = html.replace(RE_HTML_TEXT_CONTENT, (fullMatch, textContent) => {
    if (!textContent)
      return fullMatch;
    let newTextContent = textContent;
    for (const [emoji, svg] of emojiToSvg) {
      if (svg) {
        const escaped = emoji.replace(RE_REGEX_SPECIAL_CHARS, "\\$&");
        newTextContent = newTextContent.replace(new RegExp(escaped, "g"), svg);
      }
    }
    return `>${newTextContent}<`;
  });
  island.html = html;
}
