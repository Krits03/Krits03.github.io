import { defineEventHandler } from "#nuxtseo/h3";
import { getNitroOrigin } from "#site-config/server/composables/getNitroOrigin";
import { getSiteConfig } from "#site-config/server/composables/getSiteConfig";
import { useSchemaOrgConfig } from "../../utils/config.js";
export default defineEventHandler(async (e) => {
  const nitroOrigin = getNitroOrigin(e);
  const siteConfig = getSiteConfig(e);
  return {
    nitroOrigin,
    runtimeConfig: useSchemaOrgConfig(e),
    siteConfig: {
      url: siteConfig.url
    }
  };
});
