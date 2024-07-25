<script setup>
import { TresCanvas, useRenderLoop } from "@tresjs/core";
import { ref, shallowRef } from "vue";

const { onLoop } = useRenderLoop();

const cubeRef = shallowRef();
onLoop(({ delta, elapsed }) => {
  cubeRef.value.rotation.y += delta;
  cubeRef.value.rotation.z = elapsed;

  cubeRef.value.position.y = Math.sin(elapsed) * 2;
  cubeRef.value.scale.set(
    Math.sin(elapsed) * 2,
    Math.sin(elapsed) * 2,
    Math.sin(elapsed) * 2
  );
});
</script>

<template>
  <h1 style="color: 'red'">teste</h1>
  <TresCanvas clear-color="#82dbc5" window-size>
    <TresPerspectiveCamera :position="[1, 2, 4]" :look-at="[0, 0, 0]" />
    <TresMesh ref="cubeRef" :position="[0, 1, 0]">
      <TresBoxGeometry :args="[1, 1, 1]" />
      <TresMeshNormalMaterial color="teal" />
    </TresMesh>
    <TresAxesHelper />
  </TresCanvas>
</template>

<style></style>
