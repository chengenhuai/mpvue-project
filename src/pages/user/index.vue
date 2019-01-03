<template>
<div class="container" :hidden='Isshow'>
  <div class="container-userDetail-header"></div>
  <div class="container-userDetail-message">
    <dl>
      <dt>
        <img :src="user.pic">
      </dt>
      <dd>
        <span>{{user.nickname}}</span>
        <span>NO.{{user.other_no}}</span>
      </dd>
    </dl>
    <div class="container-userDetail-message-content">
      会员价 免费早餐 延时退房14:00 预定保留18:00
    </div>
  </div>
  <div class="container-userDetail-nav">
    <div>
      <span>微信会员</span>
      <span>会员</span>
    </div>
    <div @click='couPon'>
      <span>30张</span>
      <span>优惠券</span>
    </div>
    <div>
      <span>0</span>
      <span>余额</span>
    </div>
  </div>
  <div class="container-userDetail-feature">
    <div class="container-userDetail-feature-h5">
      功能
    </div>
    <div class="container-userDetail-feature-Article">
      <dl>
        <dt>
          <img src="../../images/indent.png" alt="">
        </dt>
        <dd>全部订单</dd>
      </dl>
      <dl>
        <dt>
          <img src="../../images/hotel.png" alt="">
        </dt>
        <dd>待入住</dd>
      </dl>
      <dl>
        <dt>
          <img src="../../images/message.png" alt="">
        </dt>
        <dd>评价</dd>
      </dl>
    </div>
  </div>
</div>
</template>
<script>
export default {
  data () {
    return {
      user: {
        pic: null,
        nickname: null,
        other_no: null
      },
      Isshow: true
    }
  },
  onShow () {
    let login = wx.getStorageSync('login')
    if (!login) {
      wx.redirectTo({ url: '../fail/main' })
    } else {
      this.Isshow = false
    }
  },
  onLoad () {
    wx.showLoading()
    // 当前自身的数据
    wx.request({
      url: 'https://easy-mock.com/mock/5b61a0332205a5414ac525da/example/user',
      method: 'GET',
      dataType: 'json',
      success: (res) => {
        this.user = res.data.result
      },
      fail: () => {},
      complete: () => {
        wx.hideLoading()
      }
    })
  },
  methods: {
    couPon () {
      wx.navigateTo({ url: '../coupon/main' })
    }
  }
}
</script>

<style>
.container{
  background: #eee;
}
.container .container-userDetail-header{
  width:100%;
  height: 200rpx;
  background: #6ebbff;
}
.container .container-userDetail-message{
  width:90%;
  margin:0 auto;
  background: #fff;
  position: relative;
  top: -100rpx;
  border-radius: 10rpx;
  box-shadow:1px 1px 1px #888888;
  z-index: 10;
}
.container .container-userDetail-message dl{
  width:100%;
  display: flex;
}
.container .container-userDetail-message dl dt{
  width:120rpx;
  height: 120rpx;
  display: block; 
  border-radius: 50%;
  margin: 20rpx;
}
.container .container-userDetail-message dl dt img{
  width:100%;
  height: 100%;
  border-radius: 50%;
}
.container .container-userDetail-message dl dd{
  flex:1;
  line-height: 50rpx;
  margin-top: 40rpx;
  font-size: 30rpx;
}
.container .container-userDetail-message dl dd span{
  width:100%;
  display: block;
}
.container .container-userDetail-message .container-userDetail-message-content{
  width:100%;
  color:#9e9e9e;
  font-size: 28rpx;
  height:60rpx;
  line-height: 60rpx;
  padding-left: 30rpx;
  box-sizing: border-box;
}
.container .container-userDetail-nav{
  width:100%;
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 100rpx;
  background: #fff;
  padding:80rpx 0;
  position: relative;
  top: -220rpx;
}
.container .container-userDetail-nav div{
  flex:1;
  border-right:3px solid #ccc;
  margin-top: 120rpx;
}
.container .container-userDetail-nav div:last-child{
  border-right:none;
}
.container .container-userDetail-nav div span:nth-of-type(1){
  color:red;
}
.container .container-userDetail-nav div span{
  display: block;
  text-align: center;
  font-size: 30rpx;
  line-height: 50rpx;
}
.container .container-userDetail-feature{
  width:100%;
  background: #fff;
  position: relative;
  top: -250rpx;
}
.container .container-userDetail-feature .container-userDetail-feature-h5{
  width:100%;
  height: 100rpx;
  line-height: 100rpx;
  text-align: center;
  font-size: 25rpx;
  color:#9e9e9e;
}
.container .container-userDetail-feature .container-userDetail-feature-Article{
  width:100%;
  display: flex;
  flex-wrap: wrap;
  padding-bottom: 80rpx;
}
.container .container-userDetail-feature .container-userDetail-feature-Article dl{
  flex:1;
  border-right: 1px solid #ccc;
}
.container .container-userDetail-feature .container-userDetail-feature-Article dl:nth-of-type(3){
  border-right:none;
}
.container .container-userDetail-feature .container-userDetail-feature-Article dl dt{
  width: 40rpx;
  height: 40rpx;
  margin:0 auto;
}
.container .container-userDetail-feature .container-userDetail-feature-Article dl dt img{
  width: 100%;
  height: 100%;
}
.container .container-userDetail-feature .container-userDetail-feature-Article dl dd{
  text-align: center;
  width: 100%;
  font-size: 28rpx;
  margin-top: 10rpx;
}
</style>
