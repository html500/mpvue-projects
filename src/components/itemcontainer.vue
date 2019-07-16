<template>
  <div class="container">
    <image :src="bg" class="image"></image>
    <div class="cont">
      <div class="tip-container">
        <image class="image" src="/static/images/WechatIMG2.png"></image>
        <div class="tip-txt" v-if="type == 'home'">{{ level }}</div>
        <div class="tip-txt" v-if="type == 'item'">题目{{ itemNum }}</div>
      </div>
      <div class="home-container" v-if="type == 'home'">
        <image src="/static/images/1-2.png" class="big-img"></image>
        <a class="start-btn" href="/pages/item/main">
          <image src="/static/images/1-4.png" class="image"></image>
        </a>
      </div>
      <div class="item-container" v-if="type == 'item'">
        <div class="q-list">
          <image class="image" src="/static/images/2-1.png"></image>
          <div class="list-container" v-if="itemDetail.length > 0">
            <div class="list-txt title">{{ itemDetail[itemNum-1].topic_name }}</div>
            <ul class="list">
              <li v-for="(item, index) in itemDetail[itemNum-1].topic_answer" v-bind:key="item.topic_answer_id" class="list-txt list-item" @click="chooseItem(item.topic_answer_id)">
                <span :class="chooseId == item.topic_answer_id ? 'selected' : ''">{{ index == 0 ? 'A' : index == 1 ? 'B' : index == 2 ? 'C' : 'D' }}</span>
                <span>{{ item.answer_name }}</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="start-btn next-btn">
          <image src="/static/images/3-1.png" class="image" v-if="itemNum >= itemDetail.length" @click="submitHandler"></image>
          <image src="/static/images/2-2.png" class="image" v-else @click="nextHandler"></image>
        </div>
      </div>
    </div>
    <!-- 弹窗 -->
    <toast />
  </div>
</template>

<script>
import store from '../store/store'
import toast from './toast'

export default {
  name: 'itemcontainer',
  props: ['type'],
  data () {
    return {
      bg: '/static/images/1-1.jpg', // 页面背景图url
      chooseId: '', // 选中的id
      toastText: '', // 弹窗文案
      toastShow: false // 弹窗是否展示
    }
  },
  components: {
    toast
  },
  computed: {
    level () {
      return store.state.level
    },
    itemNum () {
      return store.state.itemNum
    },
    itemDetail () {
      return store.state.itemDetail
    },
    timer () {
      return store.state.timer
    }
  },
  created () {
    if (this.type === 'home') {
      store.dispatch('initializeData')
      // this.bg = '/static/images/4-1.jpg'
    }
  },
  methods: {
    // 点击选中
    chooseItem (id) {
      this.chooseId = id
    },
    // 点击下一步
    nextHandler () {
      if (this.chooseId) {
        store.dispatch('addNum', this.chooseId)
        this.chooseId = ''
      } else {
        store.dispatch('showToast', '请选择选项！')
      }
    },
    // 点击提交
    submitHandler () {
      store.dispatch('addNum', this.chooseId)
      wx.redirectTo({
        url: '/pages/score/main'
      })
    }
  }
}
</script>

<style>
.container{
  width: 100%;
  height: 100%;
  position: relative;
}
.container .image{
  width: 100%;
  height: 100%;
}
.container .cont{
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
}
.container .cont .tip-container{
  width: 152rpx;
  height: 344rpx;
  position: absolute;
  top: 0;
  right: 74rpx;
}
.container .cont .tip-container .tip-txt{
  position: absolute;
  bottom: 48rpx;
  left: 0;
  width: 100%;
  text-align: center;
  font-weight: 600;
  color: #a57c50;
  font-size: 26rpx;
}
.container .cont .home-container, .container .cont .item-container{
  position: absolute;
  top: 300rpx;
  left: 50%;
  transform: translate3d(-50%, 0, 0);
  display: flex;
  flex-direction: column;
  align-items: center;
}
.container .cont .home-container .big-img, .container .cont .item-container .q-list{
  width: 600rpx;
  height: 560rpx;
  margin-bottom: 40rpx;
  position: relative;
}
.container .cont .start-btn{
  width: 200rpx;
  height: 100rpx;
}
.container .cont .item-container .q-list .list-container{
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-sizing: border-box;
  padding-top: 60rpx;
}
.container .cont .item-container .q-list .list-container .list-txt{
  min-width: 150rpx;
  font-size: 30rpx;
  line-height: 48rpx;
  color: #fff;
  margin-bottom: 10rpx;
}
.container .cont .item-container .q-list .list-container .list-item{
  display: flex;
  align-items: center;
}
.container .cont .item-container .q-list .list-container .title{
  font-weight: 600;
  color: red;
}
.container .cont .item-container .q-list .list-container .list-txt span:first-of-type{
  border: 2rpx solid #fff;
  color: blue;
  border-radius: 100%;
  width: 50rpx;
  height: 50rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 10rpx;
}
.container .cont .item-container .q-list .list-container .list-txt .selected{
  background: orange;
}
</style>
