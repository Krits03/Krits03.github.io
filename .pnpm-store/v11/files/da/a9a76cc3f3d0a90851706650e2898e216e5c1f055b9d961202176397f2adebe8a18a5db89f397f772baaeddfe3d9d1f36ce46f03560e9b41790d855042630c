import { join } from "pathe";
import { HINTS_ROUTE } from "../core/server/types.js";
import { createHintsLogger } from "../logger.js";
export const logger = createHintsLogger("htmlValidate");
export const HTMLVALIDATE_ROUTE = join(HINTS_ROUTE, "html-validate");
export function addBeforeBodyEndTag(html, content) {
  const closingBodyTagIndex = html.lastIndexOf("</body>");
  if (closingBodyTagIndex === -1) {
    return html + content;
  }
  return html.slice(0, closingBodyTagIndex) + content + html.slice(closingBodyTagIndex);
}
