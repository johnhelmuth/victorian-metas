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
</style>