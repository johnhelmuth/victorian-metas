<script lang="ts" setup>
import TableOfContents from "~/components/table-of-contents.vue";

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
    <DropDownBreadCrumbs :key="$route.path" hide-if-only-one />
    <TableOfContents :key="$route.path" :toc="page?.body?.toc" />
    <ContentRenderer v-if="page" :value="page"/>
    <div v-else>Page not found</div>
  </div>
</template>

<style scoped>
.content-block {
  overflow-y: auto;
}
</style>