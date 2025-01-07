<script lang="ts" setup>
import type {PrismicLinkProps} from "@prismicio/vue"

defineProps<PrismicLinkProps>()
</script>

<template>
  <PrismicLink
    v-bind="$props"
    class="buttonLink"
  >
    <slot />
  </PrismicLink>
</template>

