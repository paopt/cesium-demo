<script setup>
import { Cartesian3, createOsmBuildingsAsync, Ion, Math as CesiumMath, Terrain, Viewer, Color, GeoJsonDataSource } from 'cesium';
import { onMounted } from 'vue'
import { TOKEN } from '@/config'

// 查看器/场景/实体/数据源

onMounted(() => {
  init()
})


// 初始化cesium
async function init() {
  Ion.defaultAccessToken = TOKEN;
  const viewer = new Viewer('container', {
    timeline: false,
    animation: false,
    baseLayerPicker: false,
    geocoder: false,
    homeButton: false,
    infoBox: false,
    navigationHelpButton: false,
  });

  // viewer.scene.globe.show = false
  console.log(viewer)

  // const entity = viewer.entities.add({
  //   position: Cartesian3.fromDegrees(116.397428, 39.90923, 400),
  //   point: {
  //     pixelSize: 100,
  //     color: Color.YELLOW,
  //     outlineColor: Color.BLACK,
  //     outlineWidth: 2,
  //   },
  // })
  // viewer.trackedEntity = entity

  viewer.dataSources.add(GeoJsonDataSource.load('assets/SampleData/ne_10m_us_states.topojson'))
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
