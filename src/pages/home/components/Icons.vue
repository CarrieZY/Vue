<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <swiper-slide v-for="(page,index) of pages" :key="index">
        <div class="icon" v-for="item in page" :key="item.id">
          <div class="icon-img">
            <img class="icon-imgcontent" :src="item.imgUrl">
          </div>
          <p class="icon-desc">{{item.desc}}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
  export default {
    name: "HomeIcons",
    props: {
      list: Array
    },
    data() {
      return {
        swiperOption: {
          autoplay: false
        }
      }
    },
    computed: {
      pages() {
        const pages = []
        this.list.forEach(function (item, index) {
          const page = Math.floor(index / 8)
          if (!pages[page]) {
            pages[page] = []
          }
          pages[page].push(item)
        })
        return pages
      }
    }
  }
</script>

<style lang="stylus" scoped>
  @import '../../../assets/styles/varibles.sty'
  @import '../../../assets/styles/mixins.styl'
  .icons >>> .swiper-container
    height: 0
    padding-bottom: 50%

  /*swiper-container自带了overflow：hidden的特性*/
  /*overflow: hidden*/
  .icons
    margin-top: .1rem

    .icon
      position: relative
      overflow: hidden
      width: 25%;
      float: left
      height: 0
      padding-bottom: 25%
      .icon-img
        position: absolute
        top: 0
        left: 0
        right: 0
        bottom: .44rem
        padding: .1rem
        .icon-imgcontent
          height: 100%
          display: block
          margin: 0 auto
      .icon-desc
        height: .44rem
        position absolute
        left: 0
        bottom 0
        right: 0
        line-height: .44rem
        color: $textcolor
        text-align center
        ellipse()
</style>
