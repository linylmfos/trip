<template>
    <div>
        <div class="search">
            <input class="search-input"  v-model="keyword" type="text" placeholder="输入城市名或拼音">
        </div>
        <div class="search-content" ref="wrapper" v-show="keyword">
            <ul>
                <li class="search-item border-bottom" v-for="item of list" :key="item.id" @click="handleCityClick(item.name)">{{item.name}}</li>
                <li class="search-item border-bottom" v-show="hasNoData">没有找到匹配城市</li>
            </ul>
        </div>
    </div>  
</template>

<script>
import Bscroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'
export default {
  name: 'CitySearch',
  props:{
      cities:Object
  },
  data () {
      return {
        keyword: '',
        list:[],
        timer: null
      }
  },
   computed: {
      hasNoData () {
          return !this.list.length
      }
  },
  watch: {
      keyword () {
          if (this.timer) {
              clearInterval (this.timer)
          }
          if (!this.keyword) {
              this.list = []
              return
          }
          var _this = this
          var cities = this.cities
          this.timer = setTimeout(() => {
              const result = []
              for (let i in cities) {
                  cities[i].forEach((value) => {
                      if (value.spell.indexOf(_this.keyword) > -1 || value.name.indexOf(_this.keyword) > -1){
                          result.push(value)
                      }
                  })
              }
              _this.list = result
          },100)
      }
  },
  methods: {
   handleCityClick (city) {
      this.changeCity(city)
      setTimeout(() => {
        this.$router.push('/')
      },500)
    },
    ...mapMutations(['changeCity'])
  },
  mounted () {
      this.scroll = new Bscroll(this.$refs.wrapper)
  }
}
</script>

<style lang="scss" scoped>
 @import '~styles/varibles.scss';
 .search{
     height: .72rem;
     padding: 0 .1rem;
     background-color: $bgColor;
     text-align: center;
      @include boxShadow($bgColor);
     .search-input{
         box-sizing: border-box;
         height: .62rem;
         line-height: .62rem;
         width: 90%;
         text-align: center;
         border-radius: 1rem;
         color: #666;
         padding: 0 .2rem;
     }
 }
 .search-content{
     overflow: hidden;
     position: absolute;
     top: 1.58rem;
     left: 0;
     right: 0;
     bottom: 0; 
     background: #eee;
     z-index: 1;
     .search-item{
         line-height: .76rem;
         padding-left: .2rem;
         color: #666;
         background-color: #fff;
     }
 }
</style>

