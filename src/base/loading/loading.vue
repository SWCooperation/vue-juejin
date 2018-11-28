<template>
  <transition name="fade">
    <div class="loading" v-show="visible">
      <i class="iconfont icon-loading"> </i>
    </div>
  </transition>
</template>

<script type="text/ecmascript-6">
  export default {
    data() {
      return {
        visible: false,
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
  .loading
    position: absolute
    top: 0
    bottom: 0
    left: 0
    right: 0
    display: flex
    justify-content: center
    align-items: center
    background: rgba(0, 0, 0, 0.5)
    &.fade-enter-active, &.fade-leave-active
      transition: opacity .3s
    &.fade-enter, &.fade-leave-to
      opacity: 0
    .icon-loading
      color: #fff
      font-size: 50px
      animation: loading-rotate 2s linear infinite
      @keyframes loading-rotate {
        from { transform: rotate(0) }
        to { transform: rotate(2turn) }
      }
</style>
