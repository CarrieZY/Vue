<template>
  <div class="list" ref="wrapper">
    <div>
      <div class="area">
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
            <div class="button">{{this.currentCity}}</div>
          </div>
        </div>
      </div>
      <div class="area">
        <div class="title border-topbottom">热门城市</div>
        <div class="button-list">
          <div class="button-wrapper" v-for="item of hot" :key="item.id"
               @click="handleCityClick(item.name)">
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>
      <div class="area" v-for="(item,key) of cities" :key="key" :ref="key">
        <div class="title border-bottom">{{key}}</div>
        <div class="item-list">
          <div class="item border-bottom" v-for="innerItem of item" :key="innerItem.id"
          @click="handleCityClick(innerItem.name)">{{innerItem.name}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'
  import {mapState ,mapMutations} from 'vuex'
  export default {
    name: "CityList",
    props: {
      hot: Array,
      cities: Object,
      letter: String
    },
    computed:{
      ...mapState({
        currentCity:'city'
      })
    },
    methods :{
      handleCityClick(city){
       // this.$store.commit('changeCity',city)
        this.changeCity(city)
        this.$router.push('/')
      },
      ...mapMutations(['changeCity'])
    },
    mounted() {
      this.scroll = new BScroll(this.$refs.wrapper)
    },
    watch: {
      letter() {
        if (this.letter) {
          const element = this.$refs[this.letter][0]
          console.log(element)
          this.scroll.scrollToElement(element)
        }
      }
    }
  }
</script>

<style lang="stylus" scoped>
  @import '../../../assets/styles/varibles.sty'
  /*设置伪类可以对一像素的边框进行颜色设置*/
  .border-topbottom
    &:before
      border-color: #ccc
    &:after
      border-color #ccc

  .border-bottom
    &:before
      border-color: #ccc

  /*将页面的滚动条除掉*/
  .list
    overflow hidden
    position absolute
    left: 0
    top: 1.58rem
    right: 0
    bottom 0
    .title
      line-height: .44rem
      font-size .26rem
      background: #eee
      padding-left .2rem
      color: #666

    .button-list
      overflow hidden
      padding .1rem .6rem .1rem .1rem
      .button-wrapper
        width: 33.33%
        float left

        .button
          text-align center
          margin: .1rem
          border: .02rem solid #ccc
          background: #ffffff
          padding .1rem 0
          border-radius .06rem

    .item-list
      .item
        line-height: .54rem
        padding-left .2rem
        line-height .76rem


</style>
