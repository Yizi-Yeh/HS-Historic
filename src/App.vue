
<template>
  <div id="app">
    <!-- 側欄元件 -->
    <asideMenu/>
    <Historicmap/>
     <lightbox />
  </div>
</template>
<script>
import { mapActions } from 'vuex'
import asideMenu from './components/asideMenu'
import Historicmap from './components/Historicmap'
import lightbox from './components/lightbox'
export default {
  name: 'App',
  components: {
    asideMenu,
    Historicmap,
    lightbox
  },
  methods: {
    ...mapActions(['fetchHistoric'])
  },
  mounted () {
    this.fetchHistoric()
  }
}
</script>
<style lang="scss" src="./style.scss"></style>
