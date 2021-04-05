<template>
  <div class="Historic-map" id="Historic-map"></div>
</template>

<script>
import L from 'leaflet'
export default {
  name: 'Historicmap',
  data () {
    return {
      map: {}
    }
  },
  watch: {
    // 切換古蹟列表，與地圖中心做連動
    currHistoricInfo (item) {
      //  this.map.panTo 指向地圖中心
      const vm = item[0]
      this.map.panTo(new L.LatLng(vm['緯度'], vm['經度']))
    },
    filteredHistoric (Historic) {
      Historic.forEach((element) => this.addMarker(element))
    }
  },
  computed: {
    // 抓出目前所選的古蹟資訊
    currHistoricInfo () {
      return this.$store.getters.currHistoricInfo
    },
    filteredHistoric () {
      return this.$store.getters.filteredHistoric
    }
  },
  methods: {
    addMarker (item) {
      // 標記的圖示
      const ICON = {
        // 設定 icon 圖片路徑
        iconUrl: 'https://raw.githubusercontent.com/pointhi/leaflet-color-markers/master/img/marker-icon-2x-violet.png',
        // 設定陰影圖片路徑
        shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/0.7.7/images/marker-shadow.png',
        // 資料為陣列，設定寬度與高度
        iconSize: [25, 41],
        // 資料為陣列，設定 icon 的 X 軸與 Y 軸偏移量
        iconAnchor: [12, 41],
        // 資料為陣列，設定彈跳視窗的 X 軸與 Y 軸偏移量
        popupAnchor: [1, -34],
        // 資料為陣列，設定陰影圖片的寬度與高度
        shadowSize: [41, 41]
      }
      // 將標記放置到地圖上
      const marker = L.marker([item.緯度, item.經度], ICON)
        .addTo(this.map)
        .bindPopup(`<h2 class="popup-name">${item.古蹟名稱}</h2>`)
        .openPopup()
      // 替 marker 加入 id 與經緯度資訊
      marker.lng = item.經度
      marker.lat = item.緯度
    }
  },
  mounted () {
    // 地圖初始化
    this.map = L.map('Historic-map', {
      center: [120, 24],
      // 地圖的放大級別，數值為 0 ~ 20
      zoom: 18
    })
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '<a target="_blank" href="https://www.openstreetmap.org/">© OpenStreetMap 貢獻者</a>',
      maxZoom: 20
    }).addTo(this.map)
  }
}
</script>
