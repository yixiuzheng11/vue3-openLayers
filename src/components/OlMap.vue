<script setup>
  import { ref, onMounted } from 'vue' // vue相关方法
  import { Map, View } from 'ol'      // 地图实例方法、视图方法
  import Tile from 'ol/layer/Tile'    // 瓦片渲染方法
  import OSM from 'ol/source/OSM'    // OSM瓦片【OSM不能在实际开发中使用，因为OSM里中国地图的边界有点问题！！！！】
  import 'ol/ol.css'                 // 地图样式

  defineProps({
    msg: String
  })

  const map = ref(null) // 存放地图实例
  function initMap () {
    // 地图实例
    map.value = new Map({
      target: 'map',                         // 对应页面里 id 为 map 的元素
      layers: [                              // 图层
        new Tile({                           // 使用瓦片渲染方法
          source: new OSM()                  // 图层数据源
        })
      ],
      view: new View({                       // 地图视图
        projection: "EPSG:4326",             // 坐标系，有EPSG:4326和EPSG:3857
        center: [114.064839, 22.548857],     // 深圳坐标
        minZoom:10,                          // 地图缩放最小级别
        zoom: 12                             // 地图缩放级别（打开页面时默认级别）
      })
    })
  }
  onMounted(() => {
    initMap()
  })
</script>

<template>
  <h1>{{ msg }}</h1>
  <div id="map" class="map__x"></div>
</template>

<style scoped>
  .map__x {
    width: 600px;
    height: 600px;
    border: 1px solid #eee;
  }
</style>
