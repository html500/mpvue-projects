<template>
  <div class="item-container">
    <itemcontainer type="item"></itemcontainer>
  </div>
</template>

<script>
import itemcontainer from '@/components/itemcontainer'

export default {
  name: 'item',
  components: {
    itemcontainer
  }
}
</script>

<style scoped>
.item-container{
  width: 100vw;
  height: 100vh;
  position: relative;
}
</style>
