<template>
  <div v-if="showFullScreenBtn" class="action fullScreen">
    <a-tooltip :content="value ? '退出全屏' : '全屏'" placement="bottom">
      <a-icon @click="handleChange" :type="value ? 'fullscreen' : 'fullscreen-exit'" :size="30"></a-icon>
    </a-tooltip>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  name: 'Fullscreen',
  computed: {
    showFullScreenBtn () {
      return window.navigator.userAgent.indexOf('MSIE') < 0
    }
  },
  props: {
    value: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    handleFullscreen () {
      let main = document.body
      if (this.value) {
        if (document.exitFullscreen) {
          document.exitFullscreen()
        } else if (document.mozCancelFullScreen) {
          document.mozCancelFullScreen()
        } else if (document.webkitCancelFullScreen) {
          document.webkitCancelFullScreen()
        } else if (document.msExitFullscreen) {
          document.msExitFullscreen()
        }
      } else {
        if (main.requestFullscreen) {
          main.requestFullscreen()
        } else if (main.mozRequestFullScreen) {
          main.mozRequestFullScreen()
        } else if (main.webkitRequestFullScreen) {
          main.webkitRequestFullScreen()
        } else if (main.msRequestFullscreen) {
          main.msRequestFullscreen()
        }
      }
    },
    handleChange () {
      this.handleFullscreen()
    }
  },
  mounted () {
    let isFullscreen = document.fullscreenElement || document.mozFullScreenElement || document.webkitFullscreenElement || document.fullScreen || document.mozFullScreen || document.webkitIsFullScreen
    isFullscreen = !!isFullscreen
    document.addEventListener('fullscreenchange', () => {
      this.$emit('input', !this.value)
      this.$emit('on-change', !this.value)
    })
    document.addEventListener('mozfullscreenchange', () => {
      this.$emit('input', !this.value)
      this.$emit('on-change', !this.value)
    })
    document.addEventListener('webkitfullscreenchange', () => {
      this.$emit('input', !this.value)
      this.$emit('on-change', !this.value)
    })
    document.addEventListener('msfullscreenchange', () => {
      this.$emit('input', !this.value)
      this.$emit('on-change', !this.value)
    })
    this.$emit('input', isFullscreen)
  }
}
</script>

<style lang="less"> 
.fullScreen{
  padding:10px;
}
</style>
