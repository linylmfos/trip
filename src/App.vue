<template>
  <div id="app">
    <keep-alive>
      <router-view/>
    </keep-alive>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style lang="scss">
  .wrapper .swiper-pagination-bullet-active{
    background-color: #fff;
  }
</style>

