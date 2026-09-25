<script setup>
import { computed, resolveComponent, toRef } from "vue";
import { createSitePathResolver } from "../composables/utils";
const { canonical, absolute, withBase, ...props } = defineProps({
  canonical: { type: Boolean, required: false },
  absolute: { type: Boolean, required: false },
  withBase: { type: Boolean, required: false },
  to: { type: String, required: false },
  href: { type: String, required: false },
  external: { type: Boolean, required: false },
  target: { type: [String, null], required: false },
  rel: { type: [String, null], required: false },
  noRel: { type: Boolean, required: false },
  prefetchedClass: { type: String, required: false },
  prefetch: { type: Boolean, required: false },
  noPrefetch: { type: Boolean, required: false }
});
const resolverOptions = {
  canonical: toRef(() => canonical),
  absolute: toRef(() => absolute),
  withBase: toRef(() => withBase)
};
const linkResolver = createSitePathResolver(resolverOptions);
const NuxtLink = resolveComponent("NuxtLink");
const resolvedTo = computed(() => {
  const _to = props.to;
  if (!_to)
    return void 0;
  return linkResolver(_to);
});
</script>

<template>
  <NuxtLink v-bind="props" :to="resolvedTo" :aria-label="props.to || props.href">
    <slot />
  </NuxtLink>
</template>
