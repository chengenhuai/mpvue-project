<template>
<div class='userEquity'>
  <div class='userEquity-dl' @click='skipEquity'>
    <div class='userEquity-dl-dt'>
        <img src='../images/user_01.png'/>
  </div>
    <div class='userEquity-dl-dd'>
        会员权益
    </div>
  </div>
  <div class='userEquity-dl' @click='skipPath'>
    <div class='userEquity-dl-dt'>
        <img src='../images/user_02.png'/>
    </div>
    <div class='userEquity-dl-dd'>
        优惠券
    </div>
  </div>
  <div class='userEquity-dl' @click='dialogArise'>
    <div class='userEquity-dl-dt'>
        <img src='../images/user_03.png'/>
    </div>
    <div class='userEquity-dl-dd'>
        服务
    </div>
  </div>
  <div :class="[dialogIndex ? 'dialog' : 'dialog animation']" :hidden='dialogIndex'>
    开发中敬请期待
  </div>
</div>
</template>

<script>
export default {
  data () {
    return {
      dialogIndex: true
    }
  },
  methods: {
    skipPath () {
      wx.navigateTo({ url: '../coupon/main' })
    },
    dialogArise () {
      this.dialogIndex = false
      setTimeout(() => {
        this.dialogIndex = true
      }, 1500)
    },
    skipEquity () {
      wx.navigateTo({ url: '../equity/main' })
    }
  }
}
</script>

<style>
.userEquity{
  width:100%;
  display: flex;
  flex-wrap: wrap;
  margin-top: 20rpx;
  background: #fff;
  padding:40rpx 0;
}
.userEquity .userEquity-dl{
  flex:1;
  border-right:1px solid #ccc;
}
.userEquity .userEquity-dl:nth-of-type(3){
  border:none;
}
.userEquity .userEquity-dl .userEquity-dl-dt{
  width:80rpx;
  height:60rpx;
  margin: 0 auto;
}
.userEquity .userEquity-dl .userEquity-dl-dt img{
  width:100%;
  height:100%;
}
.userEquity .userEquity-dl .userEquity-dl-dd{
  margin-top: 10rpx;
  font-size: 30rpx;
  width:100%;
  text-align: center;
}
.userEquity .dialog{
  position: fixed;
  width:200rpx;
  height: 60rpx;
  line-height: 60rpx;
  top: 50%;
  left: 50%;
  margin-left: -100rpx;
  margin-top: -30rpx;
  z-index: 10;
  background: rgba(0,0,0,.8);
  color:#fff;
  font-size: 25rpx;
  text-align: center;
}
.animation{
  transform: 1s;
}
</style>
