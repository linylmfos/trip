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
              <div class="button-wrapper" v-for="item of hot" :key="item.id" @click="handleCityClick(item.name)">
                <div class="button">{{item.name}}</div>
              </div>
          </div>
        </div>

        <div class="area" v-for="(item,key) of cities" :key="key" :ref="key">
          <div class="title border-topbottom">{{key}}</div>
          <div class="item-list">
            <div class="item border-bottom" v-for="innerItem of item" :key="innerItem.id" @click="handleCityClick(innerItem.name)">{{innerItem.name}}</div>
          </div>
        </div>
        
      </div>  
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'
export default {
  name: "CityList",
  props: {
    hot: Array,
    cities: Object,
    letter:String
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper)
  },
  watch :{
    letter () {
      if(this.letter) {
        const element = this.$refs[this.letter][0]
        this.scroll.scrollToElement(element)
      }
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
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  }
};
</script>

<style lang="scss" scoped>
@import "~styles/varibles.scss";
.list {
  position: absolute;
  overflow: hidden;
  top: 1.58rem;
  left: 0;
  right: 0;
  bottom: 0;
  .area {
    .title {
      line-height: 0.6rem;
      font-style: 0.26rem;
      background: #eee;
      padding-left: 0.2rem;
      color: #666;
    }
    .border-topbottom {
      &::before,
      &::after {
        border-color: #ccc;
      }
    }
    .button-list {
      padding: 0.1rem 0.6rem 0.1rem 0.1rem;
      overflow: hidden;
      .button-wrapper {
        float: left;
        width: 33.33%;
        .button {
          padding: 0.15rem 0.1rem;
          margin: 0.1rem;
          text-align: center;
          border: 0.02rem solid rgba($bgColor,.1);
          border-radius: 0.1rem;
          color: rgba($bgColor,.5);
          background-color: rgba($bgColor,.2);
        }
      }
    }
    .item-list {
      .item {
        line-height: 0.76rem;
        color: #666;
        padding-left: 0.2rem;
      }
      .border-bottom {
        &::before {
          border-color: #ccc;
        }
      }
    }
  }
}
</style>


