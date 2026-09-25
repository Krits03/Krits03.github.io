import { defineNuxtModule } from '@nuxt/kit';
import { hookNuxtSeoProDataUpload } from './pro.mjs';
import 'nuxt-site-config/kit';
import 'ofetch';
import 'std-env';
import './kit.mjs';
import 'node:url';
import 'pathe';
import 'pkg-types';

const module$1 = defineNuxtModule({
  meta: {
    name: "nuxtseo-shared",
    configKey: "nuxtSeoShared",
    compatibility: {
      nuxt: ">=3.16.0"
    }
  },
  setup() {
    hookNuxtSeoProDataUpload();
  }
});

export { module$1 as default };
