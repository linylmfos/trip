<template>
  <div class="icons">
     <swiper class="swiper" :options="swiperOption">
          <swiper-slide v-for="(page,index) of pages" :key="index">
            <div class="icon" v-for="item of page" :key="item.id">
                <div class="icon-img"> <img :src="item.imgUrl" alt=""></div>
                <p class="icon-desc">{{item.desc}}</p>
            </div>
          </swiper-slide>  
      </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  props:{
      list: Array
  },
  data (){
      return{
           swiperOption:{
               autoplay: false
           }
      }
  },
  computed:{
      pages () {
          const pages= [];
          this.list.forEach((item,index) => {
              const page = Math.floor(index / 8)
              if(!pages[page]){
                  pages[page]=[]
              }
              pages[page].push(item)
          })
          return pages
      }
  }
}
</script>

<style lang="scss" scoped>
   @import '~styles/varibles.scss';
  .icons{
      overflow: hidden;
      height: 0;
      padding-bottom: 50%;
      .swiper{
          overflow: hidden;
          height: 0;
          padding-bottom: 50%;
      }
      .icon{
          overflow: hidden;
          float: left;
          width: 25%;
          height: 0;
          padding-bottom: 25%;
          position: relative;
          .icon-img{
              position: absolute;
              top: 0;
              left: 0;
              right: 0;
              bottom: .1rem;
              box-sizing: border-box;
              padding: .1rem;
              display: flex;
              img{
                  display: block;
                  margin: auto;
                  width: 65%;
              }
          }
          .icon-desc{
             position: absolute;
              left: 0;
              right: 0;
              bottom: 0;
              height: .44rem;
              line-height: .44rem;
              color:$darkTextColor;
              text-align: center;
              @include ellipsis()
          } 
      }
  }
</style>


