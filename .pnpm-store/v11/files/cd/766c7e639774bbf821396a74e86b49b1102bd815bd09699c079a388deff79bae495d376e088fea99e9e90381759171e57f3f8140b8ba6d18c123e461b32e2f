import { getBotDetection as getBotDetectionFromHeaders, getBotInfo as getBotInfoFromHeaders, isBot as isBotFromHeaders } from "@nuxtjs/robots/util";
import { getHeaders } from "#nuxtseo/h3";
import { useNitroApp } from "#nuxtseo/nitro";
function resolveBotDetectionInput(event) {
  const headers = getHeaders(event) || {};
  const nitroApp = useNitroApp();
  return { headers, patternMap: nitroApp._robotsPatternMap };
}
export function getBotDetection(event) {
  const { headers, patternMap } = resolveBotDetectionInput(event);
  return getBotDetectionFromHeaders(headers, patternMap);
}
export function isBot(event) {
  const { headers, patternMap } = resolveBotDetectionInput(event);
  return isBotFromHeaders(headers, patternMap);
}
export function getBotInfo(event) {
  const { headers, patternMap } = resolveBotDetectionInput(event);
  return getBotInfoFromHeaders(headers, patternMap);
}
