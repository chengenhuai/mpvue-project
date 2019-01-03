<template>
<div class="container">
  <div class="container-city-search">
    <div class="container-city-search-input">
      <img src="../../images/search.png" alt="">
      <input type="text" placeholder="请输入城市关键字" :value='cityName' @input='changeValue' confirm-type='go'>
    </div>
    <div class="container-city-search-text" @click='searchOrcancel'>{{name == '搜索' ? '搜索' : '取消'}}</div>
  </div>
  <h4 class="container-h4">城市选择</h4>
  <div class="container-city-content">
    <div v-for='item in city' :key='index' class="container-city-content-text">
      <div @click='changeContent' :data-name='item.name' :data-id='item.code'>{{item.name}}</div>
    </div>
  </div>
</div>
</template>
<script>
export default {
  data () {
    return {
      name: '搜索',
      city: [],
      cityName: null
    }
  },
  onLoad () {
    wx.showLoading()
    // city城市
    wx.request({
      url: 'https://api.panguoyun.com/developers/wechat/gh_d38a1683ae09/app/cities',
      method: 'GET',
      dataType: 'json',
      success: (res) => {
        this.city = res.data.result
      },
      fail: () => {},
      complete: () => {
        wx.hideLoading()
      }
    })
  },
  methods: {
    changeValue (e) {
      if (e.target.value.length !== 0) {
        this.cityName = e.target.value
        this.name = '取消'
      }
    },
    searchOrcancel () {
      if (this.name === '取消') {
        this.cityName = null
      } else {}
    },
    changeContent (e) {
      this.cityName = e.currentTarget.dataset.name
      wx.setStorageSync('value', this.cityName)
      wx.setStorageSync('city', this.cityName)
      wx.setStorageSync('cityId', e.currentTarget.dataset.id)
      setTimeout(() => {
        wx.navigateBack()
      }, 500)
    }
  }
}
</script>

<style scoped>
.container {
  width:100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}
.container .container-city-search{
  width:100%;
  height: 100rpx;
  display: flex;
  flex-wrap: wrap;
  background: #fff;
}
.container .container-city-search div{
  height:100%;
}
.container .container-city-search .container-city-search-input{
  position: relative;
  flex:8;
}
.container .container-city-search .container-city-search-input img{
  position: absolute;
  width:30rpx;
  height:30rpx;
  left: 50rpx;
  top: 35rpx;
  z-index:10;
}
.container .container-city-search .container-city-search-input input{
  width:90%;
  height:60rpx;
  background: #f5f5f5;
  margin:20rpx auto;
  padding-left: 60rpx;
  font-size: 30rpx;
  box-sizing: border-box;
}
.container .container-city-search .container-city-search-text{
  flex:2;
  text-align: center;
  line-height: 100rpx;
  font-size: 30rpx;
  color:#9e9e9e;
}
.container .container-h4{
  width:100%;
  height:100rpx;
  line-height: 100rpx;
  padding-left:20rpx;
  box-sizing: border-box;
  font-size: 35rpx;
  background: #f7f7f7;
}
.container .container-city-content{
  width:100%;
  display: flex;
  background: #fff;
  flex-wrap: wrap;
  padding-top:40rpx;
  padding-bottom: 60rpx;
}
.container .container-city-content .container-city-content-text{
  display: inline-block;
  width:25%;
  border-bottom: 1px solid #ccc;
  box-sizing: border-box;
  padding:20rpx 0;
}
.container .container-city-content .container-city-content-text div{
  display: inline-block;
  width:100%;
  height: 50rpx;
  line-height: 50rpx;
  font-size: 30rpx;
  text-align: center;
  border-right: 2px solid #ccc;
}
.container .container-city-content .container-city-content-text:nth-child(4n){
  border-right: none;
}
</style>
