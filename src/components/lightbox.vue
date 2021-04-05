<template>
  <transition name="modal">
      <div class="modal-img" v-show="showModal">
          <div class="modal-wrapper" @click.self="close"></div>
            <div class="modal-container">
                <div class="modal-body">
                  <h1 class="Historic-name" v-if="filteredHistoric.length">古蹟種類: {{ filteredHistoric[0].種類 }}</h1>
                    <h1 class="Historic-name" v-if="filteredHistoric.length">古蹟名稱: {{ filteredHistoric[0].古蹟名稱 }}</h1>
                    <hr>
                    <h1 class="Historic-name" v-if="filteredHistoric.length">圖片網址: <br> {{ filteredHistoric[0].圖片URL }}</h1>
                    <img v-if="filteredHistoric.length" :src="filteredHistoric[0].圖片URL" alt="">
                </div>
                <button @click.self="close">關閉視窗</button>
            </div>
      </div>
  </transition>
</template>
<script>
export default {
  name: 'Lightbox',
  computed: {
    showModal: {
      get () {
        return this.$store.state.showModal
      },
      set (value) {
        return this.$store.commit('setshowModal', value)
      }
    },
    filteredHistoric () {
      return this.$store.getters.filteredHistoric
    }
  },
  methods: {
    close () {
      this.showModal = false
    }
  }
}
</script>
<style lang="scss" scoped>
.modal-img {
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .65);
  display: table;
  transition: opacity .3s ease;
}
.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}
.modal-container {
  width: 520px;
  margin: 0px auto;
  padding: 10px 30px;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .3);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
}
.modal-body {
  color: #cea774;
  margin: 20px 0;
}
</style>
<style>
.modal-enter {
  opacity: 0;
}
.modal-leave-active {
  opacity: 0;
}
.modal-enter .modal-container,
.modal-leave-active .modal-container {
  transform: scale(1.1);
}
</style>
<style lang="scss" scoped>
.Historic-name {
  font-size: 1.6rem;
  font-weight: bold;
  line-height: 1.5;
}
.title{
  font-weight: 500;
  margin-bottom: .5rem;
  line-height: 1.7;
}
</style>
