<template>
  <div>
    <home-header></home-header>
    <home-swiper :list="swiperLsit"></home-swiper>
    <home-icons :list="iconList"></home-icons>
    <home-recommend :list="recommendList"></home-recommend>
    <home-weekend :list="wenkendList"></home-weekend>
  </div>
</template>

<script>
  import HomeHeader from './components/HomeHeader'
  import HomeSwiper from './components/HomeSwiper'
  import HomeIcons from './components/Icons'
  import HomeRecommend from './components/Recommend'
  import HomeWeekend from './components/Wenkend'
  import axios from 'axios'
  import {mapState} from 'vuex'

  export default {
    name: "Home",
    components: {
      HomeHeader,
      HomeSwiper,
      HomeIcons,
      HomeRecommend,
      HomeWeekend
    },
    data() {
      return {
        lastCity:'',
        swiperLsit: [],
        iconList: [],
        recommendList: [],
        wenkendList: []
      }
    },
    computed:{
      ...mapState(['city'])
    },
    methods: {
      getHomeInfo() {
        axios.get('/api/index.json?city='+this.city)
          .then(this.getHomeInfoSucc)
      },
      getHomeInfoSucc(res) {
        res = res.data
        if (res.ret && res.data) {
          const data = res.data
          this.swiperLsit = data.swiperLsit
          this.iconList = data.iconList
          this.recommendList = data.recommendList
          this.wenkendList = data.wenkendList
        }
        console.log(res)
      }
    },
    mounted() {
      // console.log('mounted')
      this.lastCity=this.city
      this.getHomeInfo()
    },
    activated (){
      // console.log('activated')
      if (this.lastCity !== this.city){
        this.lastCity =this.city
        this.getHomeInfo()
      }
    }
  }
</script>

<style scoped>

</style>
