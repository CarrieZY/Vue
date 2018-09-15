<template>
  <div>
    <div class="recommend-title">周末推荐</div>
    <ul>
      <li class="item" v-for="item in list" :key="item.id">
        <div class="item-img-wrap">
          <img :src="item.imgUrl" alt="" class="item-img">
        </div>
        <div class="item-info">
          <p class="item-title">{{item.title}}</p>
          <p class="item-desc">{{item.desc}}</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: "HomeWenkend",
    props: {
      list: Array
    }
  }
</script>

<style lang="stylus" scoped>
  @import '../../../assets/styles/mixins.styl'
  .recommend-title
    line-height .8rem
    background #eee
    text-indent .2rem

  .item-img-wrap
    height: 0
    overflow hidden
    padding-bottom 37.09%
    .item-img
      width: 100%

  .item-info
    .item-title
      line-height: .54rem
      font-size: .32rem
      color: $textColor
    .item-desc
      line-height .4rem
      color: #cccccc
      ellipse()
</style>
