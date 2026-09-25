import { defineWebPage, defineWebSite } from "@unhead/schema-org/vue";
import { defineNuxtPlugin, useError } from "nuxt/app";
import { toValue } from "vue";
import { useSiteConfig } from "#site-config/app/composables/useSiteConfig";
import { useSchemaOrg } from "../composables/useSchemaOrg.js";
import { maybeAddIdentitySchemaOrg } from "../utils/shared.js";
export default defineNuxtPlugin({
  name: "nuxt-schema-org:defaults",
  dependsOn: [
    "nuxt-schema-org:init"
  ],
  setup() {
    const error = useError();
    if (error.value?.error) {
      return;
    }
    const siteConfig = useSiteConfig();
    useSchemaOrg([
      defineWebSite({
        name: () => toValue(siteConfig.name) || "",
        inLanguage: () => toValue(siteConfig.currentLocale) || "",
        description: () => toValue(siteConfig.description) || ""
      }),
      defineWebPage()
    ]);
    maybeAddIdentitySchemaOrg();
  }
});
