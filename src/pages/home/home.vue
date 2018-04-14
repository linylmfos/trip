<template>
  <div>
      <home-header></home-header>
      <div class="home-content" ref="wrapper">
         <div>
            <home-swiper :list="swiperList"></home-swiper>
            <home-icons :list="iconList"></home-icons>
            <home-recommend :list="recommendList"></home-recommend>
            <home-weekend :list="weekendList"></home-weekend>
         </div>
      </div>
     
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
import HomeHeader from './components/Header'
import HomeSwiper from './components/Swiper'
import HomeIcons from './components/Icons'
import HomeRecommend from './components/Recommend'
import HomeWeekend from './components/Weekend'
import axios from 'axios'
import { mapState } from 'vuex'

export default {
  name: 'Home',
  components: {
    HomeHeader,
    HomeSwiper,
    HomeIcons,
    HomeRecommend,
    HomeWeekend
  },
  data () {
    return {
      lastCity:'',
      swiperList:[],
      iconList:[],
      recommendList:[],
      weekendList:[]
    }
  },
  computed: {
    ...mapState(['city'])
  },
  methods:{
    getHomeInfo () {
       axios.get('/api/index.json?city='+ this.city)
         .then(this.getHomeInfoSucc)
    },
    getHomeInfoSucc (res) {
      res = res.data
      if(res.ret && res.data){
        const data = res.data
        this.swiperList = data.swiperList
        this.iconList = data.iconList
        this.recommendList = data.recommendList
        this.weekendList = data.weekendList
      }
    }
  },
  mounted () {
    this.lastCity = this.city
    this.scroll = new Bscroll(this.$refs.wrapper)
    this.getHomeInfo()
  },
  activated () {
    if(this.lastCity != this.city){
      this.listCity = this.city
      this.getHomeInfo()
    }
   
  }
}
</script>

<style lang="scss" scoped>
@import "~styles/varibles.scss";
.home-content{
  position: absolute;
  overflow: hidden;
  top: $headerHeight;
  left: 0;
  right: 0;
  bottom: 0;
}
</style>

