<template>
  <p class="toast" v-show="show && text">
    {{ text }}
  </p>
</template>

<script>
import store from '../store/store'

export default {
  computed: {
    show () {
      return store.state.show
    },
    text () {
      return store.state.text
    }
  }
}
</script>

<style scope>
.toast {
  min-width: 400rpx;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate3d(-50%, -50%, 0);
  padding: 10px;
  animation: fadeIn 3s;
  animation-fill-mode: both;
  font-size: 30rpx;
  background: rgba(0, 0, 0, 0.4);
  text-align: center;
  color: #fff;
  border-radius: 20rpx;
}
@keyframes fadeIn{
  0%{
    display: block;
    opacity: 0;
  }
  25%{
    display: block;
    opacity: 1;
  }
  75%{
    display: block;
    opacity: 1;
  }
  100%{
    display: none;
    opacity: 0;
  }
}
</style>
