<template>
  <VueFlow v-model="elements" fit-view-on-init>
    <MiniMap />
  </VueFlow>
  <button id="logPositions" @click="logPositions">Log</button>
  <ContentDrawer :selected-id="selectedId" />
</template>

<script setup lang="ts">
import '@alexlit/css-material-color-palette-variables'
import '@vue-flow/core/dist/style.css'
import '@vue-flow/core/dist/theme-default.css'
import '@vue-flow/minimap/dist/style.css'

import { VueFlow } from '@vue-flow/core';
import { MiniMap } from '@vue-flow/minimap';
import { ref } from 'vue';

const foo = await queryContent('/').find()
// const { data: queried } = await useAsyncData('elementary', () => queryContent('elementary').findOne())

const nodeId = {
  elementary: 'elementary',
};

// build this initial object using markdown & front-matter instead
// position, type, and id can be in front-matter
// label is h1 and details (shown in side drawer when clicked) are written in md body
const elements = ref([
  {
    id: '1',
    type: 'input',
    label: 'Levels of Reading',
    position: { x: 0, y: 0 },
  },
  { id: 'e1-2', source: '1', target: 'elementary' },
  {
    id: nodeId.elementary,
    label: 'Elementary Reading',
    position: { x: -310, y: 90 },
    class: 'readingLevel readingLevel--elementary',
    selectable: true,
  },
  {
    id: '2.1',
    label: 'Reading Readiness',
    position: { x: 22, y: 75 },
    parentNode: nodeId.elementary,
    class: 'readingLevel__child',
  },
  {
    id: '2.2',
    label: 'Reading Very Simple Materials',
    position: { x: 200, y: 75 },
    parentNode: nodeId.elementary,
    class: 'readingLevel__child',
  },
  {
    id: '2.3',
    label: 'Vocabulary Building & "Unlocking" Unknown Words',
    position: { x: 380, y: 75 },
    parentNode: nodeId.elementary,
    class: 'readingLevel__child',
  },
  {
    id: '2.4',
    label: 'Refinement & Enhancement of Learned Skills',
    position: { x: 570, y: 75 },
    parentNode: nodeId.elementary,
    class: 'readingLevel__child',
  },
  { id: 'e2-3', source: 'elementary', target: '3' },
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
const selectedId = computed(() =>
  elements.value.find((elem: any) => elem.selected)?.id
)

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

  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color-scheme: light dark;
  color: rgba(255, 255, 255, 0.87);
  background-color: #242424;

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;
}
#__nuxt {
  height: 100vh;
  width: 100%;
}
@media (prefers-color-scheme: light) {
  :root {
    color: #213547;
    background-color: #ffffff;
  }
  a:hover {
    color: #747bff;
  }
  button {
    background-color: #f9f9f9;
  }
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
  width: 750px;
}
.readingLevel__child {
  background-color: var(--childNodeBgColor);
  border-color: var(--childNodeBorderColor);
}
pre {
  position: absolute;
  top: 0;
  left: 0;
  white-space: break-spaces;
  width: 600px;
  background: #00000088;
}
</style>
