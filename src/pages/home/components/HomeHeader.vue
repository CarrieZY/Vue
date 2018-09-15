<template>
  <div class="header">
    <div class="heaer-left">
      <span class="iconfont back-icon">&#xe624;</span>
    </div>
    <div class="header-input">
      <span class="iconfont">&#xe632;</span>
      输入城市/游戏主题
    </div>
    <router-link to="/city">
      <div class="header-right">
        {{this.city}}<span class="iconfont arrow-icon">&#xe64a;</span></div>
    </router-link>
  </div>

</template>

<script>
  import { mapState } from 'vuex'
  export default {
    name: "HomeHeader",
    computed:{
      ...mapState(['city'])
    }
  }
</script>

<style lang="stylus" scoped>
  @import '../../../assets/styles/varibles.sty'
  .header
    line-height: $headerHeight
    display: flex
    background: $bgColor
    color: #ffffff
    .header-left
      width: .64rem
      float: left
      .back-icon
        text-align: center
        font-size: .4rem
    .header-input
      flex: 1
      height: .64rem
      background: #ffffff
      margin-left: .2rem
      padding-left: .2rem
      margin-top: .12rem
      line-height: .64rem
      border-radius: .1rem
      color: #ccc
    .header-right
      float: right
      padding 0 .1rem
      min-width: 1.04rem
      text-align: center
      color: #fff
    .arrow-icon
      font-size: .24rem
      margin-left: -.04rem
</style>
