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

  viewer.camera.setView({
    destination: position,
    // 视角
    // orientation: {
    //   heading: Cesium.Math.toRadians(0),
    //   pitch: Cesium.Math.toRadians(0),
    //   roll: Cesium.Math.toRadians(0),
    // }
  })

  // 飞行
  // viewer.camera.flyTo({
  //   destination: position,
  //   // 视角
  //   orientation: {
  //     heading: Cesium.Math.toRadians(0),
  //     pitch: Cesium.Math.toRadians(0),
  //     roll: Cesium.Math.toRadians(0),
  //   },
  //   duration: 5
  // })
  const center =  new Cesium.Cartesian3.fromDegrees(116.39, 39.91)
  const heading =  Cesium.Math.toRadians(50)
  const pitch =  Cesium.Math.toRadians(-90)
  const range = 2000

  viewer.camera.lookAt(center, new Cesium.HeadingPitchRange(heading, pitch, range))
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
