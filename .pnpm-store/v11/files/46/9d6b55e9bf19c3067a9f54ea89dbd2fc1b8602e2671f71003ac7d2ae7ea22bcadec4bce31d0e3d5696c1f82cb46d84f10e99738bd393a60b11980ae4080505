import { EMOJI_CODEPOINT_TO_NAME } from "./emoji-names-minimal.js";
const RE_VARIATION_SELECTOR = /-fe0f$/i;
export const RE_MATCH_EMOJIS = /(?:\p{Extended_Pictographic}|[\d#*]\uFE0F\u20E3|\p{Regional_Indicator}{2})(?:\p{Emoji_Modifier}|\uFE0F|\u200D[\p{Extended_Pictographic}\p{Emoji}])*/gu;
export function getEmojiIconNames(codePoint, _emojiSet) {
  const baseCodePoint = codePoint.replace(RE_VARIATION_SELECTOR, "");
  const knownName = EMOJI_CODEPOINT_TO_NAME[codePoint] || EMOJI_CODEPOINT_TO_NAME[baseCodePoint];
  if (knownName) {
    return [knownName];
  }
  return [codePoint, baseCodePoint, `u${baseCodePoint}`].filter((v, i, a) => a.indexOf(v) === i);
}
export function getEmojiCodePoint(emoji) {
  return Array.from(emoji, (char) => char.codePointAt(0).toString(16)).join("-");
}
