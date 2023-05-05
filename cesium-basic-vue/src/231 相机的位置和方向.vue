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
  viewer.camera.setView(
    {
      // 指定相机位置
      destination: position,
      // 指定相机视角
      orientation: {
        // 指定相机方向
        heading: Cesium.Math.toRadians(90.0),
        // 指定相机倾斜角 俯仰角  -90度朝下
        pitch: Cesium.Math.toRadians(-20.0),
        // 指定相机拉近角 翻滚角
        roll: 0,
      }
    }
  )
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
