<script lang="ts" setup>

const route = useRoute()
const { data: page } = await useAsyncData(route.path, () => {
  return queryCollection('content').path(route.path).first()
})

useSeoMeta({
  title: page.value?.title,
  description: page.value?.description
})

</script>

<template>
  <div class="content-block">
    <ContentRenderer v-if="page" :value="page"/>
    <div v-else>Page not found</div>
  </div>
</template>
