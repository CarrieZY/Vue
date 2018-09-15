<template>
  <ul class="list">
    <li class="item" v-for="item of letters" :key="item" @click="handleLetterClick"
        @touchstart.prevent="handleTouchstart"
        @touchmove="handleTouchMove"
        @touchend="handleTouchEnd"
        :ref="item"
    >{{item}}
    </li>
  </ul>
</template>

<script>
  export default {
    name: "CityAlpabet",
    props: {
      cities: Object
    },
    data() {
      return {
        touchStatus: false,
        startY: 0,
        time: null
      }
    },
    computed: {
      letters() {
        const letters = []
        for (let i in this.cities) {
          letters.push(i)
        }
        return letters
      }
    },
    methods: {
      handleLetterClick(e) {
        this.$emit('change', e.target.innerText)
        // console.log(e.target.innerText);
      },
      handleTouchstart() {
        this.touchStatus = true
      },
      updated() {
        this.startY = this.$refs['A'][0].offsetTop
      },
      handleTouchMove(e) {
        if (this.touchStatus) {
          if (this.time) {
            clearTimeout(this.time)
          }
          //函数节流
          this.time = setTimeout(() => {
            const startY = this.startY
            const touchY = e.touches[0].clientY - 79
            const index = Math.floor((touchY - startY) / 20)
            if (index >= 0 && index < this.letters.length) {
              this.$emit('change', this.letters[index])
            }
            console.log(index);
          }, 16)


        }
      },
      handleTouchEnd() {
        this.touchStatus = false
      }
    }
  }
</script>

<style lang="stylus" scoped>
  @import '../../../assets/styles/varibles.sty'
  .list
    /*将侧边栏的内容垂直居中显示*/
    display flex
    flex-direction column
    justify-content center
    /**/
    position absolute
    right: 0
    top: 1.58rem
    bottom 0
    width: .4rem
    .item
      /*文字水平居中*/
      text-align center
      line-height: .4rem
      color: #25a4bb
</style>
