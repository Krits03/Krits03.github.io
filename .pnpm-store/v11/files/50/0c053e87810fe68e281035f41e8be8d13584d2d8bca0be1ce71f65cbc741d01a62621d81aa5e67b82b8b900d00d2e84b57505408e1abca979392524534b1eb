const RE_QUOT = /&quot;/g;
const RE_APOS_DEC = /&#39;/g;
const RE_APOS_HEX = /&#x27;/g;
const RE_LT = /&lt;/g;
const RE_GT = /&gt;/g;
const RE_CENT = /&cent;/g;
const RE_POUND = /&pound;/g;
const RE_YEN = /&yen;/g;
const RE_EURO = /&euro;/g;
const RE_COPY = /&copy;/g;
const RE_REG = /&reg;/g;
const RE_SLASH_HEX = /&#x2F;/g;
const RE_DEC_ENTITY = /&#(\d+);/g;
const RE_AMP = /&amp;/g;
export function htmlDecodeQuotes(html) {
  return html.replace(RE_QUOT, '"').replace(RE_APOS_DEC, "'").replace(RE_APOS_HEX, "'");
}
export function decodeHtml(html) {
  return html.replace(RE_LT, "<").replace(RE_GT, ">").replace(RE_CENT, "\xA2").replace(RE_POUND, "\xA3").replace(RE_YEN, "\xA5").replace(RE_EURO, "\u20AC").replace(RE_COPY, "\xA9").replace(RE_REG, "\xAE").replace(RE_QUOT, '"').replace(RE_APOS_DEC, "'").replace(RE_APOS_HEX, "'").replace(RE_SLASH_HEX, "/").replace(RE_DEC_ENTITY, (full, int) => {
    return String.fromCharCode(Number.parseInt(int));
  }).replace(RE_AMP, "&");
}
