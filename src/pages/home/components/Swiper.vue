<template>
  <div class="wrapper">
    <swiper :options="swiperOption">
        <swiper-slide v-for="item of list" :key="item.id" v-if="showSwiper">
            <img class="swiper-img" :src="item.imgUrl" >
        </swiper-slide>
        <div  class="swiper-pagination"  slot="pagination"></div>
    </swiper>
  </div>  
</template>

<script>
export default {
  name: 'HomeSwiper',
  props: {
      list: Array
  },
  data (){
      return{
          swiperOption:{
              pagination: '.swiper-pagination',
                autoplay: 3000,
                loop:true
          }
      }
  },
  computed: {
      showSwiper () {
         return this.list.length
      }
  }
}
</script>

<style lang="scss" scoped>
   
  .wrapper{
      width: 100%;
      overflow: hidden;
      height: 0;
      padding-bottom:31.25%; 
      background-color: #eee;
    .swiper-img{
        width: 100%;
    }
  }
  
</style>

