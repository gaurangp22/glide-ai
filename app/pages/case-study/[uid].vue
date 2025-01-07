<script setup lang="ts">
import { components } from '~/slices'

const prismic = usePrismic()
const route = useRoute()
const { data: page } = await useAsyncData(`case-study:${route.params.uid}` as string, () =>
  prismic.client.getByUID('case_study', route.params.uid as string)
)

useSeoMeta({
  title: page.value?.data.meta_title,
  ogTitle: page.value?.data.meta_title,
  description: page.value?.data.meta_description,
  ogDescription: page.value?.data.meta_description,
  ogImage: computed(() => prismic.asImageSrc(page.value?.data.meta_image)),
});
</script>


<template>
  <Bounded>
    <header class="relative grid w-full place-items-center text-center">
      <TriangleGrid />
      <h1 class="text-5xl font-medium md:text-7xl">
        <PrismicText :field="page?.data.company" />
        <span class="block text-lg text-yellow-500">Case Study</span>
      </h1>
      <p class="mb-4 mt-8 max-w-xl text-lg text-slate-300">
        <PrismicText :field="page?.data.description" />
      </p>
      <PrismicImage
        v-if="$prismic.isFilled.image(page?.data.cover)"
        :field="page?.data.cover"
        class="case-study__image rounded-lg opacity-0"
      />
    </header>
    <SliceZone
      wrapper="div"
      class="mx-auto mt-12 md:mt-16"
      :slices="page?.data.slices ?? []"
      :components="components"
    />
  </Bounded>
</template>
