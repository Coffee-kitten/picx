<template>
  <div class="image-viewer"
       :class="{'active': imageViewer.isShow}"
       @click="imageViewer.isShow = false"
  >
    <div class="image-box"
         v-if="imageViewer.url"
    >
      <img class="img"
           :src="imageViewer.url"
      >
    </div>
  </div>
</template>

<script lang="ts" setup>
import { computed } from 'vue'
import { useStore } from 'vuex'

const store = useStore()
const imageViewer = computed(() => store.getters.getImageViewer)
</script>

<style scoped lang="stylus">

$transition-duration = 0.3s
$transition-delay = 0s


.image-viewer {
  position fixed
  left 0
  top 0
  width 100%
  height 100%
  display flex
  align-items center
  justify-content center
  background rgba(0, 0, 0, 0)
  visibility hidden
  z-index 1000
  padding 6%
  box-sizing border-box
  transition-property visibility, background
  transition-delay $transition-delay, $transition-delay
  transition-duration $transition-duration, $transition-duration
  transition-timing-function ease, ease

  &.active {
    background rgba(0, 0, 0, 0.5)
    visibility visible

    .image-box {
      cursor zoom-out
      transform scale(1)
      padding 2px
    }
  }


  .image-box {
    position relative;
    width 60%
    height 100%
    display flex
    justify-content center
    align-items center
    transform scale(0)
    transition-property transform
    transition-delay $transition-delay
    transition-duration $transition-duration
    transition-timing-function ease


    @media (max-width: 1200px) {
      width 80%
    }

    .img {
      max-width 100%
      max-height 100%
    }
  }
}
</style>
