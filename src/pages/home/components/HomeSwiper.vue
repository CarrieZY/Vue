<template>
  <div class="wraper">
    <swiper :options="swiperOption" v-if="showSwiper">
      <swiper-slide v-for="item in list" :key="item.id">
        <img class="swiper-img" :src="item.imgUrl">
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
  export default {
    name: "HomeSwiper",
    props: {
      list: Array
    },
    data() {
      return {
        swiperOption: {
          pagination: '.swiper-pagination',
          loop: true,
        }
      }
    },
    computed: {
      showSwiper() {
        return this.list.length
      }
    }
  }
</script>

<style lang="stylus" scoped>
  .wraper >>> .swiper-pagination-bullet-active
    background: #fff !important

  .wraper
    width: 100%
    overflow: hidden
    height: 0
    padding-bottom: 26.25%
    background: #ccc
    .swiper-img
      width: 100%
</style>
