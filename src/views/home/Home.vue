<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    
    <scroll class="content">
      <home-swiper :banners="banners"/>
      <recommend-view :recommends="recommends"/>
      <feature-view/>
      <tab-control  class="tab-control" 
                    :titles="['流行','新款','精选']" 
                    @tabClick='tabClick'/>
      <good-list :goods='showGoods'/>
    </scroll>
  </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar'
  import TabControl from 'components/content/tabControl/TabControl'
  import GoodList from 'components/content/goods/GoodList'
  import Scroll from 'components/common/scroll/Scroll'

  import HomeSwiper from './childComps/HomeSwiper'
  import RecommendView from './childComps/RecommendView'
  import FeatureView from './childComps/FeatureView'

  import { getHomeMultidata, getHomeGoods } from 'network/home'


  export default {
    name: "Home",
    components: {
      NavBar,
      TabControl,
      HomeSwiper,
      RecommendView,
      FeatureView,
      GoodList,
      Scroll,
    },
    data() {
      return {
        banners: [],
        recommends: [],
        goods: {
          'pop': {page: 0, list: []},
          'new': {page: 0, list: []},
          'sell': {page: 0, list: []},
        },
        currentType: 'pop'
      }
    },
    computed: {
      showGoods() {
        return this.goods[this.currentType].list
      }
    },
    created() {
      // 1.请求多个数据
     this.getMultidata()

      // 2.请求商品数据
      this.getGoods('pop');
      this.getGoods('new');
      this.getGoods('sell');
      
    },
    methods: {
      /**
       * 事件监听相关方法
       */
      tabClick(index) {
        switch(index){
          case 0: 
            this.currentType = 'pop';
            break;
          case 1:
            this.currentType = 'new';
            break;
          case 2:
            this.currentType = 'sell';
            break;
        }
        console.log(this.currentType);
      },

      /**
       * 网络请求相关方法
       */
      getMultidata(){
        getHomeMultidata().then(res => {
          // es6箭头函数的this,在定义时就继承了定义函数的对象
          this.banners = res.data.banner.list;
          this.recommends = res.data.recommend.list;
        })
      },
      getGoods(type){
        const page = this.goods[type].page + 1;
        getHomeGoods(type, page).then((res) => {
          this.goods[type].list.push(...res.data.list);
          this.goods[type].page += 1;
        })
      }
    }
  }

</script>
<style scoped>
  #home{
    padding-top: 44px;
    height: 100vh;
    position: relative;
  }
  .home-nav{
    background-color: var(--color-tint);
    color: #ffffff;

    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9;
  }
  .tab-control{
    position: sticky;
    top: 44px;
    z-index: 9;
  }

  .content{
    overflow: hidden;

    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }
</style>