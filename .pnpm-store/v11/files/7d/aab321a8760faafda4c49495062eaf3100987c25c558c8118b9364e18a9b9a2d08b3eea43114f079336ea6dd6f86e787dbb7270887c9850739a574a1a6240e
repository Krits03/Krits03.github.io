import NuxtIsland from "#app/components/nuxt-island";
import { useNuxtApp } from "#imports";
import { logger } from "../../logger.js";
const originalSetup = NuxtIsland.setup;
const HintsNuxtIsland = Object.assign({}, NuxtIsland, {
  setup(props, ctx) {
    if (useNuxtApp().ssrContext?.islandContext) {
      logger.warn(
        `Nesting islands within islands is not recommanded for performance reasons. This leads to waterfall calls.`
      );
    }
    return originalSetup(props, ctx);
  }
});
export default HintsNuxtIsland;
