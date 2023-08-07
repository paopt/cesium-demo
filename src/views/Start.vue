<script setup>
import { Cartesian3, createOsmBuildingsAsync, Ion, Math as CesiumMath, Terrain, Viewer } from 'cesium';
import { onMounted } from 'vue'
import { TOKEN } from '@/config'

onMounted(() => {
  init()
})


// 初始化cesium
async function init() {
  Ion.defaultAccessToken = TOKEN;
  const viewer = new Viewer('container');
}

</script>

<template>
  <div id="container">
  </div>

</template>

<style scoped>

.container {
  width: 100vw;
  height: 100vh;
}
</style>
