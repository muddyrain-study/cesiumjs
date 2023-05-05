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

  // 创建一个点
  var point = viewer.entities.add({
    // 位置
    position: Cesium.Cartesian3.fromDegrees(
      113.3191,
      23.109,
      20
    ),
    // 点
    point: {
      pixelSize: 10,
      color: Cesium.Color.RED,
      outlineColor: Cesium.Color.WHITE,
      outlineWidth: 4,
    }
  })
  // 添加文字标签和广告牌 
  viewer.entities.add({
    position: Cesium.Cartesian3.fromDegrees(
      113.3191,
      23.109,
      650
    ),
    label: {
      text: '广州塔',
      font: '24px monospace',
      fillColor: Cesium.Color.WHITE,
      outlineColor: Cesium.Color.BLACK,
      // FILL 填充文字 OUTLINE 轮廓文字  FILL_AND_OUTLINE 填充+轮廓
      style: Cesium.LabelStyle.FILL_AND_OUTLINE,
      outlineWidth: 4,
      verticalOrigin: Cesium.VerticalOrigin.BOTTOM,
      pixelOffset: new Cesium.Cartesian2(0, -24),
    },

  })
  viewer.entities.add({
    position: Cesium.Cartesian3.fromDegrees(
      113.3191,
      23.109,
      750
    ),
    billboard: {
      image: "./texture/gzt.png",
      width: 50,
      height: 50,
      verticalOrigin: Cesium.VerticalOrigin.TOP,
      horizontalOrigin: Cesium.HorizontalOrigin.CENTER,
      // pixelOffset: new Cesium.Cartesian2(0, -24),
    }
  })
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
