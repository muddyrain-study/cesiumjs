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
  viewer.camera.flyTo({
    destination: position,
    duration: 3,
    orientation: {
      heading: Cesium.Math.toRadians(0.0),
      pitch: Cesium.Math.toRadians(-20.0),
      roll: Cesium.Math.toRadians(0.0),
    }
  })
  // 通过按键移动相机
  document.addEventListener("keydown", e => {
    // 获取相机离地面的高度
    var height = viewer.camera.positionCartographic.height
    var moveRate = height / 10
    switch (e.key) {
      case 'w':
        viewer.camera.moveForward(moveRate)
        break;
      case 's':
        viewer.camera.moveBackward(moveRate)
        break;
      case 'a':
        viewer.camera.moveLeft(moveRate)
        break;
      case 'd':
        viewer.camera.moveRight(moveRate)
        break;
      case 'q':
        // 设置相机向左旋转
        viewer.camera.lookLeft(Cesium.Math.toRadians(0.1))
        break
      case 'e':
        // 设置相机向右旋转
        viewer.camera.lookRight(Cesium.Math.toRadians(0.1))
        break
      case 'r':
        // 设置相机向上旋转
        viewer.camera.lookUp(Cesium.Math.toRadians(0.1))
        break
      case 'f':
        // 设置相机向下旋转
        viewer.camera.lookDown(Cesium.Math.toRadians(0.1))
        break
      case 'g':
        // 向左逆时针翻滚
        viewer.camera.twistLeft(Cesium.Math.toRadians(0.1))
        break
      case 'h':
        // 向右逆时针翻滚
        viewer.camera.twistRight(Cesium.Math.toRadians(0.1))
        break
      default:
        break;
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
