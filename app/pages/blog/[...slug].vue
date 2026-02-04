<script setup lang="ts">
import { useRoute } from 'vue-router'

const route = useRoute()

const { data: page } = await useAsyncData(() =>
  queryCollection('blog')
    .path(`/blog/${route.params.slug}`)
    .first()
)

if (!page.value) {
  throw createError({ statusCode: 404 })
}
</script>

<template>
  <ContentRenderer
    v-if="page"
    :value="page"
  />
</template>
