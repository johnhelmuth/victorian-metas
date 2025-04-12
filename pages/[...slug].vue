<script lang="ts" setup>
const route = useRoute()
const { data: page } = await useAsyncData(route.path, () => {
  return queryCollection('content').path(route.path).first()
})
</script>

<template>
  <div class="content-block">
    <ContentRenderer v-if="page" :value="page"/>
  </div>
</template>

<style scoped>
.content-block {
  overflow-y: auto;
}
</style>