<template>
<div class="container">
  <div class="container-hotel-search">
    <img src="../../images/search.png" alt="" class="img1">
    <input type="text" placeholder="搜索地址 / 酒店 / 地标" @click='skipCity'>
    <div class="container-hotel-search-site">
      <img src="../../images/site.png" alt="" class="img2">{{city}}
    </div>
  </div>
  <div class="container-hotel-nav">
    <span>美丽豪</span>
    <span>美豪</span>
    <span>雅致</span>
    <span>丽致</span>
  </div>
  <div class="container-hotel-caption">
    <span>距离</span>
    <span>评分</span>
  </div>
  <div class="container-hotel-content">
    <dl class="container-hotel-content-dl" v-for='item in Json' :data-id='item.mid' :key='index' @click='skipDetail'>
      <dt class="container-hotel-content-dl-dt">
        <img :src='item.pic' alt="">
      </dt>
      <dd class="container-hotel-content-dl-dd">
        <p>
          <span>{{item.name}}</span>
          <span>${{item.price}}起</span>
        </p>
        <p>
          地址:{{item.address}}
        </p>
        <p>
          <span>电话:{{item.tel}}</span>
          <span>{{item.star}}分</span>
        </p>
      </dd>
    </dl>
  </div>
</div>
</template>

<script>
export default {
  data () {
    return {
      Json: [],
      city: '不限'
    }
  },
  onShow () {
    let setLocal = wx.getStorageSync('cityId')
    let setName = wx.getStorageSync('city')
    if (setLocal.length !== 0) {
      this.city = setName
      wx.request({
        url: 'https://api.panguoyun.com/developers/wechat/gh_d38a1683ae09/app?city=' + setLocal,
        method: 'GET',
        dataType: 'json',
        success: res => {
          this.Json = res.data.result
        },
        fail: () => {},
        complete: () => {
          wx.hideLoading()
        }
      })
    } else {
      // 详情页
      wx.request({
        url: 'https://api.panguoyun.com/developers/wechat/gh_d38a1683ae09/app?city=&key=&brand=',
        data: 'data',
        method: 'GET',
        dataType: 'json',
        success: res => {
          this.Json = res.data.result
        },
        fail: () => {},
        complete: () => {
          wx.hideLoading()
        }
      })
    }
  },
  methods: {
    skipCity () {
      wx.navigateTo({ url: '../city/main' })
    },
    skipDetail (e) {
      wx.navigateTo({ url: '../detail/main?id=' + e.currentTarget.dataset.id })
    }
  }
}
</script>

<style>
.container{
  width:100%;
  height: 100%;
}
.container .container-hotel-search{
  width:100%;
  height: 80rpx;
  position: relative;
  flex-shrink: 0; 
}
.container .container-hotel-search .img1{
  width:30rpx;
  height: 30rpx;
  position: absolute;
  top: 15rpx;
  left: 60rpx;
}
.container .container-hotel-search .container-hotel-search-site{
  position: absolute;
  right:60rpx;
  top:10rpx;
  z-index: 10;
  font-size: 30rpx;
}
.container .container-hotel-search .container-hotel-search-site img{
  width:30rpx;
  height: 30rpx;
  margin-right: 20rpx;
}
.container .container-hotel-search input{
  width:90%;
  height: 60rpx;
  line-height: 60rpx;
  background: #e1e1e1;
  font-size: 30rpx;
  padding-left: 80rpx;
  box-sizing: border-box;
  margin: 0 auto;
}
.container .container-hotel-nav{
  width:90%;
  height: 80rpx;
  line-height: 80rpx;
  margin: 0 auto;
  font-size: 30rpx;
}
.container .container-hotel-nav span{
  border:1px solid #ccc;
  margin-right: 20rpx;
  padding: 10rpx 20rpx;
  color:#9e9e9e;
}
.container .container-hotel-caption{
  display: flex;
  flex-wrap: wrap;
  width:90%;
  height: 80rpx;
  line-height: 80rpx;
  margin: 0 auto;
  font-size: 30rpx;
  margin-top: 20rpx;
  border-bottom: 1px solid #ccc;
  flex-shrink: 0;
}
.container .container-hotel-caption span{
  flex:1;
  text-align: center;
}
.container .container-hotel-caption span:nth-of-type(1){
  border-right: 1px solid #ccc;
}
.container .container-hotel-content{
  width:90%;
  margin:0 auto;
}
.container .container-hotel-content .container-hotel-content-dl{
  width:100%;
  display: flex;
  padding:40rpx 0;
  border-bottom: 1px solid #ccc;
}
.container .container-hotel-content .container-hotel-content-dl .container-hotel-content-dl-dt{
  width:150rpx;
  height: 150rpx;
}
.container .container-hotel-content .container-hotel-content-dl .container-hotel-content-dl-dt img{
  width:100%;
  height: 100%;
}
.container .container-hotel-content .container-hotel-content-dl .container-hotel-content-dl-dd{
  flex:1;
  margin-left: 30rpx;
}
.container .container-hotel-content .container-hotel-content-dl .container-hotel-content-dl-dd p:nth-of-type(1){
  width:100%;
  display: flex;
  justify-content: space-between;
  font-weight: 550;
}
.container .container-hotel-content .container-hotel-content-dl .container-hotel-content-dl-dd p:nth-of-type(1) span:nth-of-type(1){
  font-size: 30rpx;
}
.container .container-hotel-content .container-hotel-content-dl .container-hotel-content-dl-dd p:nth-of-type(1) span:nth-of-type(2){
  font-size: 30rpx;
  color:red;
}
.container .container-hotel-content .container-hotel-content-dl .container-hotel-content-dl-dd p:nth-of-type(2){
  width:100%;
  font-size: 26rpx;
  color:#9e9e9e;
  margin-top: 40rpx;
  line-height: 40rpx;
}
.container .container-hotel-content .container-hotel-content-dl .container-hotel-content-dl-dd p:nth-of-type(3){
  width:100%;
  display: flex;
  justify-content: space-between;
  color:#9e9e9e;
  line-height: 40rpx;
  font-size: 26rpx;
}
.container .container-hotel-content .container-hotel-content-dl .container-hotel-content-dl-dd p:nth-of-type(3) span:nth-of-type(2){
  color:red;
}
</style>
