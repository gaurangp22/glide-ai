<script lang="ts" setup>
const prismic = usePrismic()
const { data: settings } = await useAsyncData("settings", () =>
  prismic.client.getSingle('settings')
)
</script>

<template>
  <div>
    <AppHeader :settings="settings" />
    <slot />
    <AppFooter :settings="settings" />
  </div>
</template>
