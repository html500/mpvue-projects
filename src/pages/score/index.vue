<template>
  <div class="score-container">
    <image src="/static/images/4-1.jpg" class="image"></image>
    <div class="cont-container">
      <div class="top-box">
        <image class="image" src="/static/images/4-2.png"></image>
        <div class="top-cont">
          <div class="score">{{ score }}分！</div>
          <div class="tip">{{ tips }}</div>
        </div>
      </div>
      <image 
        src="/static/images/4-3.png" 
        class="share-btn" 
        @click="showShare"
      ></image>
      <div class="tip-text">关注我，获取答案。</div>
      <image src="/static/images/wx_qr_code.jpg" class="qr-code"></image>
    </div>
    <div class="share-container" v-if="isShowShare" @click="closeShare">
      <image src="/static/images/5-2.png" class="tip-image" @click.stop></image>
    </div>
  </div>
</template>

<script>
// Use Vuex
import store from '../../store/store'

export default {
  data () {
    return {
      score: 0, // 分数
      tips: '', // 提示文案
      rightAnswer: [2, 7, 12, 13, 18], // 正确答案
      scoreTipsArr: [
        '你说，是不是把知识都还给小学老师了？',
        '还不错，但还需要继续加油哦！',
        '不要嘚瑟还有进步的空间！',
        '智商离爆表只差一步了！',
        '你也太聪明啦，葡萄之家欢迎你！'
      ], // 提示文案列表
      isShowShare: false // 是否展示分享提示
    }
  },
  computed: {
    answerid () {
      return store.state.answerid
    }
  },
  created () {

  },
  onShow () {
    this.computedScore()
    this.getScoreTip()
  },
  methods: {
    // 展示分享弹窗
    showShare () {
      this.isShowShare = true
    },
    // 关闭分享弹窗
    closeShare () {
      this.isShowShare = false
    },
    // 计算分数
    computedScore () {
      this.answerid.forEach((item, index) => {
        if (item == this.rightAnswer[index]) { //eslint-disable-line 
          this.score += 20
        }
      })
    },
    // 根据分数显示提示
    getScoreTip: function () {
      let index = Math.ceil(this.score / 20) - 1
      index = index > 0 ? index : 0
      this.tips = this.scoreTipsArr[index]
    }
  }
}
</script>

<style>
.score-container{
  width: 100vw;
  height: 100vh;
  position: relative;
}
.score-container .image{
  width: 100%;
  height: 100%;
}
.score-container .cont-container{
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-sizing: border-box;
  padding-top: 100rpx;
}
.score-container .cont-container .top-box{
  width: 460rpx;
  height: 440rpx;
  position: relative;
  margin-bottom: 38rpx;
}
.score-container .cont-container .top-box .top-cont{
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-sizing: border-box;
  padding: 220rpx 40rpx 0;
}
.score-container .cont-container .top-box .top-cont .score{
  height: 88rpx;
  font-size: 72rpx;
  line-height: 88rpx;
  margin-bottom: 30rpx;
  color: #a51d31;
  -webkit-text-stroke: 4rpx #412318;
  font-family: 'Microsoft YaHei';
  text-align: center;
  font-weight: 600;
}
.score-container .cont-container .top-box .top-cont .tip{
  color: #3e2415;
  text-align: center;
  font-size: 32rpx;
}
.score-container .cont-container .share-btn{
  width: 282rpx;
  height: 112rpx;
  margin-bottom: 60rpx;
}
.score-container .cont-container .tip-text{
  text-align: center;
  font-size: 24rpx;
  color: #664718;
  margin-bottom: 20rpx;
}
.score-container .cont-container .tip-text{
  text-align: center;
  font-size: 24rpx;
  color: #664718;
}
.score-container .cont-container .qr-code{
  width: 248rpx;
  height: 248rpx;
}
.score-container .share-container{
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  z-index: 2;
  display: flex;
  justify-content: center;
  box-sizing: border-box;
  padding-top: 24rpx;
  background: rgba(0, 0, 0, 0.5);
}
.score-container .share-container .tip-image{
  width: 560rpx;
  height: 314rpx;
}
</style>
