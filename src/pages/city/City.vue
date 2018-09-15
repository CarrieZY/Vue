<template>
  <div>
    <city-header></city-header>
    <city-search :cities="cities"></city-search>
    <city-list :cities="cities" :hot="hotCities" :letter="letter"></city-list>
    <city-alpabet :cities="cities" @change="handleLetterChange"></city-alpabet>
  </div>
</template>

<script>
  import CityHeader from './components/Header'
  import CitySearch from './components/Search'
  import CityList from './components/List'
  import CityAlpabet from './components/Alpabet'
  import axios from 'axios'

  export default {
    name: "City",
    components: {
      CityHeader,
      CitySearch,
      CityList,
      CityAlpabet
    },
    data() {
      return {
        cities: {},
        hotCities: [],
        letter:''
      }
    },
    methods: {
      getCityInfo() {
        axios.get('/api/city.json')
          .then(this.getCityInfoSucc)
      },
      getCityInfoSucc(res) {
        res = res.data
        if (res.ret && res.data) {
          const data = res.data
          this.cities=data.cities
          this.hotCities = data.hotCities
        }
        console.log(res)
      },
      handleLetterChange(letter){
        this.letter=letter
        console.log(letter)
      }
    },
    mounted() {
      this.getCityInfo()
    }
  }
</script>

<style scoped>

</style>
