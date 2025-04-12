<script setup lang="ts">

const route = useRoute();

type crumbType = {name: string, path?: string};

const breadCrumbs = ref([] as Array<crumbType>);

watchEffect(async () => {
  let pathForCrumb = '';
  const breadcrumbMeta = route.path.split('/').splice(1)
      .map((crumb) => {
        pathForCrumb += ('/' + crumb);
        return {crumb,pathForCrumb};
      });
  breadCrumbs.value = await Promise.all(breadcrumbMeta.map(async (crumbMeta) => {
    const crumbContent = await queryCollection('content').path(crumbMeta.pathForCrumb).first();
    const crumb = { name: crumbContent?.title || crumbMeta.crumb } as crumbType;
    if (crumbContent?.path) {
      crumb.path = crumbContent.path;
    }
    return crumb;
  }));
})


</script>

<template>
<div v-if="breadCrumbs?.length">
  <ul class="breadcrumb-list">
    <li v-for="(breadcrumb, index) in breadCrumbs" :key="`crumb-${index}`" class="breadcrumb-item">
      <NuxtLink v-if="breadcrumb?.path && index+1 < breadCrumbs.length" :to="breadcrumb.path">
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
li::after {
  content: '>';
  margin-left: 0.5rem;
  margin-right: 0.5rem;
}
li:last-child::after {
  content: none;
  margin: revert;
}
li {
  display: inline-block;
}
.breadcrumb-item:last-child, .breadcrumb-item:last-child * {
  font-weight: bold;
}
.breadcrumb-item a {
  font-style: italic;
  color: var(--color-text-lightest);
}
</style>