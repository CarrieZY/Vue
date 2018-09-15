<template>
  <div>

    <router-link tag="div" to="/" class="header-abs" v-show="showAbs">
      <div class="iconfont header-abs-back">&#xe624;</div>
    </router-link>
    <div class="header-fixed" v-show="!showAbs" :style="opacityStyle">
      <router-link tag="div" to="/" class="iconfont header-fixed-back">&#xe624;</router-link>
      景点详情
    </div>
  </div>
</template>

<script>
  export default {
    name: "DetailHeader",
    data() {
      return {
        showAbs: false,
        opacityStyle: {
          opacity: 1
        }
      }
    },
    methods: {
      handleScroll() {
        let top = document.documentElement.scrollTop
        if (top > 60) {
          let opacity = top / 140
          opacity = opacity > 1 ? 1 : opacity
          this.opacity = {opacity}
          this.showAbs = false
        } else {
          this.showAbs = true
        }
        console.log(document.documentElement.scrollTop);
      }
    },
    activated() {
      //这里是一个对全局事件的绑定 这个问题存在潜在的bug
      window.addEventListener('scroll', this.handleScroll)
    },
    //这段代码可以解绑全局事件的绑定  只对挡墙分支有作用
    deactivated(){
      window.removeEventListener('scroll',this.handleScroll)
    }
  }
</script>

<style lang="stylus" scoped>
  @import '../../../assets/styles/varibles.sty'
  .header-abs
    position absolute
    left: .2rem
    top .2rem
    width: .8rem
    height .8rem
    border-radius .4rem
    background: rgba(0, 0, 0, .8)
    line-height .8rem
    text-align center
    .header-abs-back
      color #ffffff
      font-size .4rem

  .header-fixed
    z-index:2
    position fixed
    top: 0
    left: 0
    right: 0
    height: $headerHeight
    line-height $headerHeight
    text-align center
    color: #fff
    background: $bgColor
    font-size .32rem
    .header-fixed-back
      text-align center
      position fixed
      top: 0
      left: 0
      width: .64rem
      font-size .4rem

</style>
