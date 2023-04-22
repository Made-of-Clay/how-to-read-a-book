<template>
  <div>
    <VueFlow v-model="elements" />
  </div>
</template>

<script setup lang="ts">
import { VueFlow } from '@vue-flow/core';
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
    position: { x: 0, y: 0 },
  },
  { id: 'e2-3', source: '2', target: '3' },
  {
    id: '3',
    label: 'Inspectional Reading',
    position: { x: 0, y: 0 },
  },
  { id: 'e3-4', source: '3', target: '4' },
  {
    id: '4',
    label: 'Analytical Reading',
    position: { x: 0, y: 0 },
  },
  { id: 'e4-5', source: '4', target: '5' },
  {
    id: '5',
    type: 'output',
    label: 'Synoptic Reading',
    position: { x: 0, y: 0 },
  },
]);
</script>

<style>
</style>
