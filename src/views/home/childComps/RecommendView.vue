<template>
  <div class="recommend">
    <div v-for="(item, key) in recommends" class="recommend-item">
      <a :href="item.link">
        <img :src="item.image">
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RecommendView',
  props: {
    recommends: {
      type: Array,
      default() {
        return []
      }
    }
  }
}

</script>
<style>
.recommend{
  display: flex;
  text-align: center;
  font-size: 12px;

  padding: 15px 0 20px 0;
  border-bottom: 10px solid #eee;
}

.recommend-item{
  flex: 1;
}

.recommend-item img{
  width: 68px;
  height: 68px;
  margin-bottom: 10px;
}
</style>