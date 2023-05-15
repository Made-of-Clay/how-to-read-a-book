<template>
  <div class="contentDrawer" :class="{ 'contentDrawer--showing': !!selectedId }">
    <ContentDoc v-if="path" :path="path" />
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  selectedId: {
    type: String,
    default: '',
  },
})

const path = computed(() => props.selectedId.toLowerCase())
</script>

<style>
.contentDrawer {
  --width: 620px;

  background-color: var(--gray--900);
  box-sizing: border-box;
  height: 100vh;
  max-width: var(--width);
  right: 0;
  padding: 1rem;
  position: fixed;
  transition: transform 0.3s ease-in-out;
  transform: translateX(var(--width));
  top: 0;
  width: 100%;
  z-index: 999;
}
.contentDrawer--showing {
  transform: translateX(0);
}
</style>