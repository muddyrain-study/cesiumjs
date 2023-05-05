<script setup>
import * as Cesium from "cesium"
import "cesium/Build/Cesium/Widgets/widgets.css";
import { onMounted } from "vue";

// 设置 cesium token
Cesium.Ion.defaultAccessToken = `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJjMjg5NDc4MS02MDEzLTRhNzctYWZmZS0wODBiOTY5N2Q5NWQiLCJpZCI6MTMyOTM0LCJpYXQiOjE2ODExMTM3NjV9.6gsxUzk-N7d5j4aczy86pueVrnFZGV2jtgwiYa96c9A`

// 设置静态资源路径
window.CESIUM_BASE_URL = '/'
// 设置默认视角
Cesium.Camera.DEFAULT_VIEW_RECTANGLE = Cesium.Rectangle.fromDegrees(
  // 西边经度   
  89.5,
  // 南边经度  
  20.4,
  // 东边经度  
  110.4,

  // 北边经度  
  61.2,
)

onMounted(() => {
  const viewer = new Cesium.Viewer("cesiumContainer", {
    // 是否显示信息
    infoBox: false,
  })
  // 隐藏 logo
  viewer.cesiumWidget.creditContainer.style.display = "none"

  // 瞬间到达指定位置和视角
  // 生成 position 是天安们的位置
  const position = Cesium.Cartesian3.fromDegrees(
    116.393428,
    39.90923,
    100
  )
  // 生成广州塔的位置
  var position2 = Cesium.Cartesian3.fromDegrees(
    113.3191,
    23.109,
    2000
  )
  viewer.camera.flyTo({
    destination: position2,
    orientation: {
      heading: Cesium.Math.toRadians(0.0),
      pitch: Cesium.Math.toRadians(-90.0),
      roll: Cesium.Math.toRadians(0.0),
    }
  })

  // 添加3d建筑
  const osmBuildings = viewer.scene.primitives.add(
    new Cesium.createOsmBuildings()
  )
  // 添加3d模型
  const airplane = viewer.entities.add({
    position: Cesium.Cartesian3.fromDegrees(
      113.3191,
      23.109,
      1000
    ),
    model: {
      uri: "./model/Air.glb",
      // 设置飞机最小的像素
      minimumPixelSize: 500,
      runAnimations: true,
      // 设置飞机的轮廓
      silhouetteSize: 1,
      // 轮廓的颜色
      silhouetteColor: Cesium.Color.WHITE,
      // 设置相机距离模型多远距离显示
      distanceDisplayCondition: new Cesium.DistanceDisplayCondition(
        0,
        100000
      )
    }
  })
  // viewer.zoomTo(viewer.entities)
  viewer.flyTo(viewer.entities)
})
</script>

<template>
  <div id="cesiumContainer" ref="cesiumContainer"></div>
</template>

<style >
* {
  margin: 0;
  padding: 0;
}

#cesiumContainer {
  width: 100vw;
  height: 100vh;
}
</style>
