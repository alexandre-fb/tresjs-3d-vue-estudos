<script setup>
import { TresCanvas, useRenderLoop } from "@tresjs/core";
import { OrbitControls } from '@tresjs/cientos'
import { ref, shallowRef, watchEffect } from "vue";
import { TresLeches, useControls } from '@tresjs/leches'
import '@tresjs/leches/styles'

const torusRef = shallowRef();
const { onLoop } = useRenderLoop();
onLoop(({ delta, elapsed }) => {
  if(!torusRef.value) return;

  torusRef.value.rotation.y += delta;
  torusRef.value.rotation.z += delta;
});

useControls('fpsgraph')
</script>

<template>
  <TresLeches />
  <TresCanvas clear-color="#82dbc5" window-size>
    <TresPerspectiveCamera :position="[1, 2, 4]" :look-at="[0, 0, 0]" />
    <OrbitControls />
    <TresMesh ref="torusRef" :position="[0, 0, 0]">
      <TresTorusKnotGeometry :args="[1, 0.4, 100, 16]" />
      <TresMeshNormalMaterial color="teal" />
    </TresMesh>
    <TresAxesHelper />
  </TresCanvas>
</template>

<style></style>
