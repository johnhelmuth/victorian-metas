<script setup lang="ts">
const route = useRoute();

const breadcrumbs = computed(() => {
  let pathForCurrentCrumb = '';
  return route.path.split('/').splice(1)
      .map((crumb) => {
        pathForCurrentCrumb += ('/' + crumb);
        return {
          'name': crumb,
          'path': pathForCurrentCrumb
        }
      });
});

</script>

<template>
<div v-if="breadcrumbs.length">
  <ul class="breadcrumb-list">
    <li v-for="(breadcrumb, index) in breadcrumbs" :key="`crumb-${index}`" class="breadcrumb-item">
      <NuxtLink v-if="index+1 < breadcrumbs.length" :to="breadcrumb.path">
        {{ breadcrumb.name }}
      </NuxtLink>
      <span v-else>{{ breadcrumb.name }}</span>
    </li>
  </ul>
</div>
</template>

<style scoped>
ul {
  list-style: none;
}
li::before {
  content: '/';
  margin-left: 0.5rem;
  margin-right: 0.5rem;
}
li {
  display: inline-block;
}
</style>