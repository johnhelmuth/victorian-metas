<script setup>

const SITE_TITLE = 'The Aetherions';

const page_title=ref('');

useHead({
  titleTemplate: (titleChunk) => {
    page_title.value = titleChunk;
    return page_title.value;
  }
});

</script>

<template>
  <NuxtRouteAnnouncer />
  <NuxtLayout  id="app" :site_title="SITE_TITLE" :page_title="page_title">
    <NuxtPage class="content-page"/>
  </NuxtLayout>
</template>
