<template>
  <div>
    <svg-icon :name="isFullscreen?'exit-fullscreen':'fullscreen'" @click="click" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import screenfull from 'screenfull'
const sf: any = screenfull
// import * as screenfull from 'screenfull'
// const sf: screenfull.Screenfull = screenfull.default
@Component
export default class Screenfull1 extends Vue {
  isFullscreen: boolean = false
  private mounted () {
    if (sf.enabled) {
      sf.on('change', () => {
        this.isFullscreen = sf.isFullscreen
      })
    }
  }
  private click () {
    if (!sf.enabled) {
      this.$message({
        message: 'you browser can not work',
        type: 'warning'
      })
      return false
    }
    sf.toggle()
  }
}
</script>

<style lang="sass" scoped>
.screenfull-svg
  display: inline-block
  cursor: pointer
  fill: #5a5e66
  width: 20px
  height: 20px
  vertical-align: 10px
</style>
