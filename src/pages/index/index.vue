<template>
  <div class="home-container">
    <itemcontainer type="home"></itemcontainer>
  </div>
</template>

<script>
import itemcontainer from '@/components/itemcontainer'

export default {
  name: 'home',
  components: {
    itemcontainer
  }
}
</script>

<style scoped>
.home-container{
  width: 100vw;
  height: 100vh;
  position: relative;
}

.home-container .img{
  width: 100%;
  height: 300rpx;
}
</style>
