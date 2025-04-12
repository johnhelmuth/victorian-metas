<script setup lang="ts">
const route = useRoute();
onMounted(() => console.log('route mounted.'));
</script>

<template>
  <div>
    <header>
      <NuxtLink to="/">Victorian Metapowers</NuxtLink>
    </header>
    <div v-if="route.path !=='/'" class="breadcrumb"><Breadcrumb /></div>
    <slot />
    <footer>Copyright John Helmuth 2025</footer>
  </div>
</template>

<style scoped>
header {
  margin-bottom: 1rem;
  font-size: 1.5rem;
  font-weight: bold;
}
.breadcrumb {
  margin-bottom: 1rem;
}
footer {
  font-size: 0.5rem;
  padding: 0.5rem;
}

/** Styles for elements rendered from markdown files. **/
h2, :deep(h2) {
  margin-top: 0.5rem;
  margin-bottom: 0.25rem;
  font-weight: bolder;
  font-size: 1.25rem;
}
h3, :deep(h3) {
  margin-top: 0.75rem;
  margin-bottom: 0.25rem;
  font-weight: bold;
}
p, :deep(p) {
  margin-bottom: 0.5rem;
}
strong, :deep(strong) {
  font-weight: bold;
}
blockquote, :deep(blockquote) {
  margin-left: 1rem;
  margin-right: 3rem;
  padding: 1rem;
  border: 1px var(--color-text) solid;
  border-radius: 0.5rem;
}
ul :deep(ul) {
  margin-top: 0.25rem;
}
</style>