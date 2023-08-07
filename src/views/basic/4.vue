<script setup>
import * as Cesium from 'cesium';
import { onMounted } from 'vue'
import { TOKEN } from '@/config'

// 地图、地形、建筑物

onMounted(() => {
  init()
})


// 初始化cesium
async function init() {
  Cesium.Ion.defaultAccessToken = TOKEN;
  const viewer = new Cesium.Viewer('container', {
    // timeline: false,
    // animation: false,
    // baseLayerPicker: false,
    // geocoder: false,
    // homeButton: false,
    // infoBox: false,
    // navigationHelpButton: false,
    // terrainProvider: await Cesium.CesiumTerrainProvider.fromIonAssetId(
    //   1
    // ),
  });

  // const layer = viewer.imageryLayers.addImageryProvider(
  //   await Cesium.IonImageryProvider.fromAssetId(3812)
  // );

//   const provider = await Cesium.CesiumTerrainProvider.fromIonAssetId(1)
//   viewer.scene.setTerrain(provider );
// 

// // 建筑物
// const tileset = viewer.scene.primitives.add(
//   await Cesium.Cesium3DTileset.fromIonAssetId(96188)
// );

// tileset.style = new Cesium.Cesium3DTileStyle({
//   color: 'color("blue", 0.6)',
//   show: true
// })

viewer.camera.setView({
  destination: Cesium.Cartesian3.fromDegrees(116.397428, 39.90923, 3000),
  // orientation: {
  //     heading: Cesium.Math.toRadians(120),
  //     pitch: Cesium.Math.toRadians(-50),
  //     roll: Cesium.Math.toRadians(0),
  // }
})


 // 加载空间数据
  const entity = viewer.entities.add({
    id: 'point',
    position: Cesium.Cartesian3.fromDegrees(116.397428, 39.90923, 0),
    point: {
      pixelSize: 100,
      color: Cesium.Color.YELLOW,
      outlineColor: Cesium.Color.BLACK,
      outlineWidth: 2,
    },
    description: `
      <h1>弹窗标日， 饿哦匣中风了</h1>
    `
  })
  viewer.trackedEntity = entity

  // 事件

  const handler = new Cesium.ScreenSpaceEventHandler(viewer.scene.canvas)
  handler.setInputAction(movement => {
    const pick = viewer.scene.pick(movement.position)
    if (Cesium.defined(pick) && pick.id.id === 'point') {
      alert('选中了')
    }
  }, Cesium.ScreenSpaceEventType.LEFT_CLICK)
  // const entity = viewer.entities.add({
  //   position:  Cesium.Cartesian3.fromDegrees(121.48727, 31.247, 0),
  //   label: {
  //     text: 'hello',
  //     font: '50px',
  //     fillColor: Cesium.Color.SKYBLUE
  //   }
  // })

  // 3D tiles

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
