import { defineWebPage } from "@unhead/schema-org/vue";
import { defu } from "defu";
import { defineNitroPlugin } from "#nuxtseo/nitro";
import { buildSchemaOrgContentScript } from "../../utils/content.js";
import { useSchemaOrgConfig } from "../utils/config.js";
export default defineNitroPlugin((nitroApp) => {
  const config = useSchemaOrgConfig();
  nitroApp.hooks.hook("content:file:afterParse", async (content) => {
    if (content._draft || content._extension !== "md" || content._partial || content.indexable === false || content.index === false)
      return;
    if (!content.schemaOrg) {
      return;
    }
    const script = buildSchemaOrgContentScript(content.schemaOrg, defineWebPage, config.scriptAttributes);
    content.head = defu({
      script: [script]
    }, content.head);
    return content;
  });
});
