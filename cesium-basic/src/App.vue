<template>
  <div id="cesiumContaine" ref="cesiumContainer"></div>
</template>

<script setup>
import { ref } from "vue";
import * as Cesium from "cesium";
const cesiumContainer = ref(null);
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
