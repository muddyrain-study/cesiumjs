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

  // 1 屏幕坐标系统 二维的笛卡尔坐标系 Cartesian2 类型
  // 2 地理坐标系统 WGS-84坐标系 Cartographic 类型 精度 维度 高度
  // 3 笛卡尔空间直角坐标系 Cartesian3 类型

  // 角度与弧度的转换
  var radian = Cesium.Math.toRadians(90)
  console.log(radian);
  // 弧度转角度
  var degrees = Cesium.Math.toDegrees(2 * Math.PI)
  console.log(degrees);
  // 将经纬度转为笛卡尔坐标
  var cartesian3 = Cesium.Cartesian3.fromDegrees(
    // 经度
    89.5,
    // 纬度
    20.4,
    // 高度
    100
  )
  console.log(cartesian3);
  // 将笛卡尔坐标转为经纬度
  var cartographic = Cesium.Cartographic.fromCartesian(cartesian3)
  console.log(cartographic);
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
