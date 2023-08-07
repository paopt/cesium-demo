<script setup>
import * as Cesium from 'cesium';
import { onMounted } from 'vue'
import { TOKEN } from '@/config'

// 相机

onMounted(() => {
  init()
})


// 初始化cesium
async function init() {
  Cesium.Ion.defaultAccessToken = TOKEN;
  const viewer = new Cesium.Viewer('container', {
    timeline: false,
    animation: false,
    baseLayerPicker: false,
    geocoder: false,
    homeButton: false,
    infoBox: false,
    navigationHelpButton: false,
  });

  const position = Cesium.Cartesian3.fromDegrees(116.39, 39.91, 400)
  const orientation = Cesium.Transforms.headingPitchRollQuaternion(position, new Cesium.HeadingPitchRoll(-90, 0, 0))
  const entity = viewer.entities.add({
    position: position,
    model: {
      uri: 'assets/SampleData/models/CesiumAir/Cesium_Air.glb',
      minimumPixelSize: 100,
      maximumScale: 10000,
      show: true
    }
  })
  viewer.camera.viewBoundingSphere(new Cesium.BoundingSphere(position, 20), new Cesium.HeadingPitchRange(0, 0, 0))
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
