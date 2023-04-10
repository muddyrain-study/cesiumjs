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
    // 地理编码器 搜索框
    geocoder: false,
    // 是否显示home按钮
    homeButton: false,
    // 是否显示 2d 3d切换模式按钮
    sceneModePicker: false,
    // 是否显示图形选择器
    baseLayerPicker: false,
    // 是否显示帮助按钮
    navigationHelpButton: false,
    // 是否播放动画控制
    animation: false,
    // 是否显示时间轴
    timeline: false,
    // 是否显示全屏按钮
    fullscreenButton: false,
    // 设置天空盒子
    skyBox: new Cesium.SkyBox({
      sources: {
        positiveX: './texture/sky/px.jpg',
        negativeX: './texture/sky/nx.jpg',
        positiveY: './texture/sky/ny.jpg',
        negativeY: './texture/sky/py.jpg',
        positiveZ: './texture/sky/pz.jpg',
        negativeZ: './texture/sky/nz.jpg'
      }
    })
  })
  // 隐藏 logo
  viewer.cesiumWidget.creditContainer.style.display = "none"
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
