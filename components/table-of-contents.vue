<script setup lang="ts">

import type {Toc} from "@nuxtjs/mdc";

defineProps<{
  toc: Toc | undefined
}>();

const tocIconName = 'material-symbols:toc-rounded';

const isExpanded=ref(false);

function toggleToc() {
  isExpanded.value = !isExpanded.value;
}

/**
 * Handle the scroll behavior when an item on the table of contents
 * menu is clicked.
 *
 * @param e
 */
function tocItemClicked(e: Event) {
  const target = e.currentTarget;
  if (target instanceof HTMLAnchorElement && target.href) {
    scrollToHeader(target.href);
  }
  toggleToc();
}

function scrollToHeader(href: string) {
  const hashElement = document.querySelector(href);
  if (hashElement) {
    hashElement.scrollIntoView({behavior: 'smooth'});
  }
}

</script>

<template>
  <div :class="{'table-of-contents-container': true, 'is-expanded': isExpanded}">
    <ul class="table-of-contents" v-show="isExpanded" v-if="(toc?.links?.length || 0) > 1">
      <li v-for="link of toc?.links" :key="link.id" >
        <a :href="'#' + link.id">{{ link.text }}</a>
        <ul class="table-of-contents-2" v-if="link.children">
          <li v-for="childLink of link.children" :key="childLink.id">{{ childLink.text }}>
            <a :href="'#' + childLink.id" @click="tocItemClicked">{{ childLink.text}}</a>
          </li>
        </ul>
      </li>
    </ul>
    <Icon class="expand-toc" @click="toggleToc"
          :name="tocIconName"/>
  </div>
</template>

<style scoped>

.table-of-contents-container {
  display: flex;
  flex-direction: column;
  border: 1px solid transparent;
  align-items: flex-end;
}

.table-of-contents-container .table-of-contents {
  display: none;
  position: fixed;
  background-color: var(--color-background-mute);
  border: 1px solid var(--color-border);
  padding: 2.5rem 1rem 1rem;
  list-style: none;
}

.expand-toc {
  position: fixed;
  font-size: 2.5em;
  font-weight: bolder;
  align-self: flex-end;
}

/* TODO: Add animation to slide the table of contents into view. */
.table-of-contents-container.is-expanded .table-of-contents {
  display: block;
}
</style>