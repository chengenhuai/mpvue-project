<template>
<div class="container">
  <div class="container-coupon">
    <div class="container-coupon-h5">
      优惠券
    </div>
    <div class="container-coupon-dl" v-for='item in Json' :key='index'>
      <div class="container-coupon-dl-dt">
        <span>{{item.name}}</span>
        <span>只可用于抵扣房费使用</span>
        <span>{{item.start}}-{{item.end}}</span>
      </div>
      <div class="container-coupon-dl-dd">
        <span>
          {{item.price}}<b>元</b>
        </span>
        <span>订房券</span>
      </div>
    </div>
  </div>
</div> 
</template>

<script>
export default {
  data () {
    return {
      Json: []
    }
  },
  onLoad () {
    wx.request({
      url: 'https://easy-mock.com/mock/5b61a0332205a5414ac525da/example/list',
      method: 'GET',
      dataType: 'json',
      success: (res) => {
        this.Json = res.data.result
      },
      fail: () => {},
      complete: () => {
        wx.hideLoading()
      }
    })
  }
}
</script>

<style>
.container{
  background:#eee;
}
.container .container-coupon-h5{
  width: 100%;
  height: 80rpx;
  line-height: 80rpx;
  font-size: 30rpx;
  padding-left: 20rpx;
  box-sizing: border-box;
}
.container .container-coupon-dl{
  width:90%;
  margin: 40rpx auto;
  display: flex;
  flex-wrap: wrap;
}
.container .container-coupon-dl .container-coupon-dl-dt{
  flex:7;
  background: #fff;
}
.container .container-coupon-dl .container-coupon-dl-dt span{
  display: block;
  padding-left: 10rpx;
  box-sizing: border-box;
}
.container .container-coupon-dl .container-coupon-dl-dt span:nth-of-type(1){
  width: 100%;
  font-size: 30rpx;
  line-height: 80rpx;
  height: 80rpx;
}
.container .container-coupon-dl .container-coupon-dl-dt span:nth-of-type(2),
.container .container-coupon-dl .container-coupon-dl-dt span:nth-of-type(3){
  line-height: 40rpx;
  font-size: 25rpx;
  height: 40rpx;
  color:#9e9e9e;
  overflow: hidden;
}
.container .container-coupon-dl .container-coupon-dl-dd{
  flex:3;
  text-align: center;
  background: #6ebbff;
}
.container .container-coupon-dl .container-coupon-dl-dd span{
  display: block;
  color:#fff;
}
.container .container-coupon-dl .container-coupon-dl-dd span b{
  display: inline;
  font-weight: 400;
  font-size: 25rpx;
}
.container .container-coupon-dl .container-coupon-dl-dd span:nth-of-type(1){
  font-size: 40rpx;
  line-height: 80rpx;
}
.container .container-coupon-dl .container-coupon-dl-dd span:nth-of-type(2){
  font-size: 25rpx;
  line-height: 50rpx;
}
</style>

