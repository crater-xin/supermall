<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'

export default {
  name: 'Scroll',
  components: {
    BScroll,
  },
  data(){
    return{
      scroll: null
    }
  },
  mounted() {
    console.log(this.$refs.wrapper);
    this.scroll = new BScroll(this.$refs.wrapper, {

    })
  }
}

</script>
<style scoped>
</style>