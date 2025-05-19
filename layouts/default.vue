<script setup lang="ts">
import ShieldKnotLogo from "~/components/shield-knot-logo.vue";

defineProps<{ site_title: string, page_title: string }>();

</script>

<template>
  <div class="layout-container">
    <div class="layout-parchment">
      <div class="layout-parchment-content">
        <header>
          <div class="home-link">
            <NuxtLink to="/">
              <ShieldKnotLogo class="logo"/>
            </NuxtLink>
            <NuxtLink to="/">{{ site_title }}</NuxtLink>
            <div class="hamburger-placeholder">&nbsp;</div>
          </div>
          <h1>{{ page_title }}</h1>
          <DropDownBreadCrumbs :key="$route.path" hide-if-only-one/>
        </header>
        <slot/>
        <footer>Copyright John Helmuth 2025</footer>
        <svg class="svg-filters">
          <filter id="wavy">
            <feTurbulence x="0" y="0" baseFrequency="0.02" numOctaves="5" seed="1"/>
            <feDisplacementMap in="SourceGraphic" scale="20"/>
          </filter>
        </svg>
      </div>
    </div>
  </div>
</template>

<style scoped>

.layout-parchment {
  box-shadow: 0 0 5rem var(--color-border) inset;
  background: var(--color-background);
}

.layout-parchment-content {
  backdrop-filter: url('#wavy');
  padding: 2rem 2rem 0;
}

header {
  margin-bottom: 0.25rem;
  padding: 0 1rem;
  font-size: 1.5rem;
  font-weight: bold;
  text-align: center;
}

header div.home-link {
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative;
}

header a:hover:has(.logo)  {
  color: inherit;
  background-color: inherit;
}

header div.home-link .hamburger-placeholder {
  height: 1.5rem;
  width: 1.5rem;
}

footer {
  font-size: 0.75rem;
  padding: 0.5rem;
  position: relative;
  top: 1rem;
}

/** Styles for elements rendered from markdown files. **/
h2, :deep(h2), h2 a, :deep(h2 a) {
  margin-top: 0.5rem;
  margin-bottom: 0.25rem;
  font-weight: bold;
  font-size: 1.25rem;
}

h3, :deep(h3), h3 a, :deep(h3 a) {
  margin-top: 0.75rem;
  margin-bottom: 0.25rem;
  font-weight: bold;
}

p, :deep(p) {
  margin-bottom: 0.5rem;
}

p a, :deep(p a) {
  font-style: italic;
  color: var(--color-text-lightest);
}

strong, :deep(strong) {
  font-weight: bold;
}

blockquote, :deep(blockquote) {
  margin-left: 1rem;
  margin-right: 3rem;
  margin-bottom: 1rem;
  padding: 1rem;
  border: 1px var(--color-text) solid;
  border-radius: 0.5rem;
}

ul, :deep(ul) {
  margin-top: 0.25rem;
  margin-bottom: 0.5rem;
}

.svg-filters {
  height: 0;
}

</style>