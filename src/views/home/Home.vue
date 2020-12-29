<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <home-swiper :banners="banners"/>
    <recommend-view :recommends="recommends"/>
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar'
import HomeSwiper from './childComps/HomeSwiper'
import RecommendView from './childComps/RecommendView'

import { getHomeMultidata } from 'network/home'


export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView
  },
  data() {
    return {
      banners: [],
      recommends: []
    }
  },
  created() {
    // 1.请求多个数据
    getHomeMultidata().then(res => {
      // console.log(res);
      // es6箭头函数的this,在定义时就继承了定义函数的对象
      this.banners = res.data.banner.list;
      this.recommends = res.data.recommend.list;
    })
  }
}

</script>
<style>
.home-nav{
  background-color: var(--color-tint);
  color: #ffffff;
}
</style>