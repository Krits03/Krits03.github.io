import { createConsola } from "consola";
import { isFeatureLogsEnabled } from "./core/features.js";
export function createHintsLogger(feature) {
  return createConsola({
    level: isFeatureLogsEnabled(feature) ? void 0 : 0
  }).withTag(`hints:${feature}`);
}
export const logger = createConsola().withTag("hints");
