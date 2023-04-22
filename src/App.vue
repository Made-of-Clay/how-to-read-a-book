<template>
  <VueFlow v-model="elements" fit-view-on-init>
    <MiniMap />
  </VueFlow>
  <button id="logPositions" @click="logPositions">Log</button>
</template>

<script setup lang="ts">
import { VueFlow } from '@vue-flow/core';
import { MiniMap } from '@vue-flow/minimap';
import { ref } from 'vue';

const elements = ref([
  {
    id: '1',
    type: 'input',
    label: 'Levels of Reading',
    position: { x: 0, y: 0 },
  },
  { id: 'e1-2', source: '1', target: '2' },
  {
    id: '2',
    label: 'Elementary Reading',
    position: { x: -145, y: 90 },
    class: 'readingLevel readingLevel--elementary',
  },
  {
    id: '2.1',
    label: 'Sub Component 1',
    position: { x: 14, y: 40 },
    parentNode: '2',
    class: 'readingLevel__child',
  },
  { id: 'e2-3', source: '2', target: '3' },
  {
    id: '3',
    label: 'Inspectional Reading',
    position: { x: -190, y: 360 },
    class: 'readingLevel readingLevel--inspectional',
  },
  { id: 'e3-4', source: '3', target: '4' },
  {
    id: '4',
    type: 'output',
    label: 'Analytical Reading',
    position: { x: -516, y: 650 },
    class: 'readingLevel readingLevel--analytical',
  },
  { id: 'e3-5', source: '3', target: '5' },
  {
    id: '5',
    type: 'output',
    label: 'Synoptic Reading',
    position: { x: 120, y: 650 },
    class: 'readingLevel readingLevel--synoptic',
  },
]);
function logPositions() {
  elements.value.forEach(el => {
    el.position && console.log({ id: el.id, ...el.position })
  })
}
</script>

<style>
:root {
  --parentNodeBgColor: var(--green--a100);
  --parentNodeBorderColor: var(--green--500);
  --childNodeBgColor: var(--light-blue--100);
  --childNodeBorderColor: var(--light-blue--500);
}
#logPositions {
  position: absolute;
  top: 0;
  right: 0;
}
.readingLevel {
  background-color: var(--parentNodeBgColor);
  /* background: linear-gradient(var(--parentNodeBgColor2), var(--parentNodeBgColor)); */
  border-color: var(--parentNodeBorderColor);
  height: 200px;
  width: 500px;
}
/* .readingLevel::before {
  THIS IS THE SHADOW I WANT - just need to figure out the colors in hex first
  box-shadow: 0 0 5px 4px var(--color) inset;
  content: '';
  display: block;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
} */
.readingLevel--elementary {
  /* color: white; */
}
.readingLevel__child {
  background-color: var(--childNodeBgColor);
  border-color: var(--childNodeBorderColor);
}
</style>
