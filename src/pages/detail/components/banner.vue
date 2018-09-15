<template>
  <div>
    <div class="banner" @click="handleBannerClick()">
      <img :src="bannerImg"
           class="banner-img">
      <div class="banner-info">
        <div class="banner-title">
          {{this.sightName}}
        </div>
        <div class="banner-number">
          <span class="iconfoot banner-icon">&#xe796;</span>
          {{this.gallaryImgs.length}}
        </div>
      </div>
    </div>
    <fade>
      <common-gallary :imgs="gallaryImgs" v-show="showGallary" @close="handleGallayClose"></common-gallary>
    </fade>
  </div>
</template>

<script>
  import CommonGallary from 'common/gallary/gallary'
  import Fade from 'common/fade/fade'
  export default {
    name: "DetailBanner",
    props: {
      sightName: String,
      bannerImg: String,
      gallaryImgs: Array,
      Fade
    },
    data() {
      return {
        showGallary: false,
      }
    },
    components: {
      Fade,
      CommonGallary
    },
    methods: {
      handleBannerClick() {
        this.showGallary = true
      },
      handleGallayClose() {
        this.showGallary = false
      }
    }
  }
</script>

<style lang="stylus" scoped>
  .banner
    position relative
    overflow hidden
    height: 0
    padding-bottom 55%
    .banner-img
      width: 100%
      background pink
    .banner-info
      display flex
      position absolute
      left 0
      right 0
      bottom 0
      line-height .6rem
      color #ffffff
      background-image linear-gradient(top, rgba(0, 0, 0, 0), rgba(0, 0, 0, .8))
      .banner-title
        flex 1
        font-size .32rem
        padding 0 .2rem
      .banner-number
        margin-top.14rem
        padding 0 .4rem
        line-height .32rem
        height: .32rem
        border-radius .24rem
        background rgba(0, 0, 0, .8)
        font-size .24rem
        .banner-icon
          font-size .24rem

</style>
