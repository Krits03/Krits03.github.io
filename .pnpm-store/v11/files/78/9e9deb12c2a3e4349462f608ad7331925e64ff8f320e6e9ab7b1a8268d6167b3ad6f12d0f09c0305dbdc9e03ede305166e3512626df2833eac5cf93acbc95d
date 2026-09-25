import { defineNuxtPlugin } from "#imports";
import { parse } from "devalue";
import { logger } from "./utils.js";
export default defineNuxtPlugin({
  name: "@nuxt/hints:html-validate",
  setup() {
    const el = document.getElementById("hints-html-validate");
    const raw = el?.textContent;
    if (!raw) {
      return;
    }
    let data;
    try {
      data = parse(raw);
    } catch (err) {
      logger.warn("[html-validate] Failed to parse report payload", err);
      return;
    }
    if (!data?.results || !Array.isArray(data.results)) {
      return;
    }
    for (const result of data.results) {
      result.messages.forEach((message) => {
        logger.warn(`[html-validate] ${message.ruleId} at ${result.filePath}:${message.line}:${message.column} - ${message.message}`);
      });
    }
  }
});
