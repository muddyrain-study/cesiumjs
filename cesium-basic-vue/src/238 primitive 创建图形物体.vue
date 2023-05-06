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
    // 地形提供者: 高分辨率地形，精度高达 1 米。
    terrainProvider: Cesium.createWorldTerrain(),
  })
  const osmBuildings = viewer.scene.primitives.add(Cesium.createOsmBuildings());
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

  // 使用entity创建矩形
  var rectangle = viewer.entities.add({
    rectangle: {
      coordinates: Cesium.Rectangle.fromDegrees(
        // 西边的经度
        90,
        // 南边维度
        20,
        // 东边经度
        110,
        // 北边维度
        30
      ),
      material: Cesium.Color.RED.withAlpha(0.5),
    },
  });

  // primivite创建矩形
  // 01-创建几何体
  let rectGeometry = new Cesium.RectangleGeometry({
    rectangle: Cesium.Rectangle.fromDegrees(
      // 西边的经度
      115,
      // 南边维度
      20,
      // 东边经度
      135,
      // 北边维度
      30
    ),
    // 距离表面高度
    height: 0,
    vertexFormat: Cesium.PerInstanceColorAppearance.VERTEX_FORMAT,
  });

  // 02-创建几何体实例
  let instance = new Cesium.GeometryInstance({
    geometry: rectGeometry,
    attributes: {
      color: Cesium.ColorGeometryInstanceAttribute.fromColor(
        Cesium.Color.BLUE.withAlpha(0.5)
      ),
    },
  });
  // 03-设置外观
  let appearance = new Cesium.PerInstanceColorAppearance({
    flat: true,
  });
  // 04-图元
  let primitive = new Cesium.Primitive({
    geometryInstances: instance,
    appearance: appearance,
  });
  // 05-添加到viewer
  viewer.scene.primitives.add(primitive);

  viewer.camera.setView(viewer.entities);
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
