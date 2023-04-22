<template>
  <VueFlow v-model="elements" fit-view-on-init>
    <MiniMap />
  </VueFlow>
  <!-- <button id="logPositions" @click="logPositions">Log</button> -->
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
    position: { x: 619, y: 98 },
  },
  { id: 'e1-2', source: '1', target: '2' },
  {
    id: '2',
    label: 'Elementary Reading',
    position: { x: 558, y: 238 },
  },
  { id: 'e2-3', source: '2', target: '3' },
  {
    id: '3',
    label: 'Inspectional Reading',
    position: { x: 637, y: 399 },
  },
  { id: 'e3-4', source: '3', target: '4' },
  {
    id: '4',
    label: 'Analytical Reading',
    position: { x: 615, y: 582 },
  },
  { id: 'e4-5', source: '4', target: '5' },
  {
    id: '5',
    type: 'output',
    label: 'Synoptic Reading',
    position: { x: 654, y: 771 },
  },
]);
// function logPositions() {
//   elements.value.forEach(el => {
//     el.position && console.log({ id: el.id, ...el.position })
//   })
// }
</script>

<style>
#logPositions {
  position: absolute;
  top: 0;
  right: 0;
}
</style>
