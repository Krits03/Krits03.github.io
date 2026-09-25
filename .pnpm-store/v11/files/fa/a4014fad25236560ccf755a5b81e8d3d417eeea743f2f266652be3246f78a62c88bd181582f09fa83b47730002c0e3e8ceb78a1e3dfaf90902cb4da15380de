import { splitCssDeclarations } from "../utils/css.js";
const RE_KEBAB_SEGMENT = /-([a-z])/g;
const RE_CSS_QUOTES = /^['"](.+)['"]$/;
const RE_IMPORTANT = /\s*!important\s*$/;
const RE_HTML_ENTITY = /&(?:amp|quot|#39|#x27);/g;
const HTML_ENTITY_MAP = {
  "&amp;": "&",
  "&quot;": '"',
  "&#39;": "'",
  "&#x27;": "'"
};
function camelCase(str) {
  return str.replace(RE_KEBAB_SEGMENT, (_, c) => c.toUpperCase());
}
function decodeHtmlEntities(value) {
  return value.replace(RE_HTML_ENTITY, (m) => HTML_ENTITY_MAP[m] ?? m);
}
export function parseStyleAttr(style) {
  if (!style)
    return void 0;
  const result = {};
  for (const decl of splitCssDeclarations(decodeHtmlEntities(style))) {
    const colonIdx = decl.indexOf(":");
    if (colonIdx === -1)
      continue;
    const prop = decl.slice(0, colonIdx).trim();
    const val = decl.slice(colonIdx + 1).trim();
    if (prop && val) {
      const cleanVal = val.replace(RE_IMPORTANT, "");
      result[camelCase(prop)] = prop === "font-family" ? cleanVal.replace(RE_CSS_QUOTES, "$1") : cleanVal;
    }
  }
  return Object.keys(result).length ? result : void 0;
}
