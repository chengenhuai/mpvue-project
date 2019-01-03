<template>
<div class="container">
  <div class="container-detail">
    <div class="container-detail-dl">
      <div class="container-detail-dl-dt">
        <img :src='Json.picture'/>
      </div>
      <div class="container-detail-dl-dd" @click='skipContent(hotel.app.id)'>
        <p>{{Json.name}}</p>
        <p>
          评分:
          <span>{{Json.commment.star}}分</span>
          <span>{{Json.wechat_pay}}条评论</span>
        </p>
        <p>{{Json.tel}}</p>
        <p>{{Json.address}}</p>
      </div>
    </div>
    <div class="container-detail-time">
      <div class="container-detail-time-date">
        <span>入住日期</span>
        <span></span>
        <span>离店日期</span>
      </div>
      <div class="container-detail-time-timer">
        <span>
          {{month}}月{{date}}日<span>周{{day}}</span>
        </span>
        <span>共一晚</span>
        <span>
          {{month}}月{{Tommrowdate}}日<span>周{{Tommrowday}}</span>
        </span>
      </div>
    </div>
  </div>
  <div class="container-detail-content">
    <div class="container-detail-content-li" v-for='(item, index) in hotel.types' :key='index' @click="reveal(item.tid)">
      <div class="container-detail-content-li-dl">
        <div class="container-detail-content-li-dl-dt">
          <img :src="item.pic">
        </div>
        <div class="container-detail-content-li-dl-dd">
          <p>{{item.name}}</p>
          <p>
            <span>{{item.info.width}}</span>
            <span>
              <span>{{item.price.rac}}</span>
              门市价
            </span>
          </p>
          <p>
            <span v-for='(value, key) in item.tags' :key='key'>{{value}}</span>
          </p>
        </div>
      </div>
      <div class="container-detail-li-content">
        <span>会员价</span>
        <span>{{item.price.vip}}元/间</span>
        <span>
          <span>预定</span>
        </span>
      </div>
    </div>
  </div>
  <div class="dialog" :hidden='IsHidden'>
    <div class="dialog-content-boxes">
      <div class="dialog-content-boxes-image">
        <img :src="content.pic"/>
        <p>
          <span>{{content.name}}</span>
          <span>{{content.price.vip}}/间</span>
        </p>  
        <p>
          <span>窗户</span>
          <span>有窗</span>
        </p>
        <p>
          <span>入住人数</span>
          <span>2人(不可加床)</span>
        </p>
      </div>
      <div class="dialpg-content-exit" @click="exit">x</div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  data () {
    return {
      hotel: {
        types: null
      },
      Json: {
        picture: null,
        commment: {
          star: null
        },
        name: null,
        wechat_pay: null,
        tel: null,
        address: null
      },
      month: null,
      day: null,
      date: null,
      Tommrowday: null,
      Tommrowdate: null,
      IsHidden: true,
      content: {
        name: null,
        pic: null,
        price: {
          vip: null
        }
      }
    }
  },
  onLoad (e) {
    this.month = new Date().getMonth() + 1
    this.date = new Date().getDate()
    this.Tommrowdate = new Date().getDate() + 1
    if (this.month < 10) {
      this.month = '0' + this.month
    }
    if (this.Tommrowdate < 10) {
      this.Tommrowdate = '0' + this.Tommrowdate
    }
    if (this.date < 10) {
      this.date = '0' + this.date
    }
    let day = new Date().getDay().toString()
    let Tommrowday = (new Date().getDay() + 1).toString()
    switch (day) {
      case '1':
        this.day = '一'
        break
      case '2':
        this.day = '二'
        break
      case '3':
        this.day = '三'
        break
      case '4':
        this.day = '四'
        break
      case '5':
        this.day = '五'
        break
      case '6':
        this.day = '六'
        break
      case '7':
        this.day = '日'
        break
    }
    switch (Tommrowday) {
      case '1':
        this.Tommrowday = '一'
        break
      case '2':
        this.Tommrowday = '二'
        break
      case '3':
        this.Tommrowday = '三'
        break
      case '4':
        this.Tommrowday = '四'
        break
      case '5':
        this.Tommrowday = '五'
        break
      case '6':
        this.Tommrowday = '六'
        break
      case '7':
        this.Tommrowday = '日'
        break
    }
    wx.request({
      url: 'https://api.panguoyun.com/developers/wechat/gh_d38a1683ae09/type?start=2018-' + this.month + '-' + this.date + '&end=2018-' + this.month + '-' + this.Tommrowdate + '&id=' + parseInt(e.id),
      method: 'GET',
      dataType: 'json',
      success: (res) => {
        this.Json = res.data.result.app
        this.hotel = res.data.result
      },
      fail: () => {},
      complete: () => {
        wx.hideLoading()
      }
    })
  },
  methods: {
    skipContent (e) {
      wx.navigateTo({ url: '../hoteldetail/main?id=' + e })
    },
    exit () {
      this.IsHidden = true
    },
    reveal (e) {
      this.hotel.types.map((item, index) => {
        if (item.tid === e) {
          this.content = item
        }
      })
      this.IsHidden = false
    }
  }
}
</script>

<style>
.dialog{
  width:100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background: rgba(0,0,0,.6)
}
.dialog .dialog-content-boxes{
  width:100%;
  height: 100%;
  position: relative;
}
.dialog .dialog-content-boxes .dialpg-content-exit{
  width:60rpx;
  height: 60rpx;
  background: #fff;
  color:#000;
  font-size: 40rpx;
  line-height: 60rpx;
  text-align: center;
  border-radius: 50%;
  position: fixed;
  bottom: 200rpx;
  left: 50%;
  margin-left: -20rpx;
}
.dialog .dialog-content-boxes .dialog-content-boxes-image{
  width:80%;
  position: absolute;
  left: 10%;
  top: 100rpx;
  background: #fff;
  padding-bottom: 40rpx;
  border-radius: 10rpx;
}
.dialog .dialog-content-boxes .dialog-content-boxes-image img{
  width: 100%;
  height: 550rpx;
}
.dialog .dialog-content-boxes .dialog-content-boxes-image p{
  width: 90%;
  margin: 0 auto;
}
.dialog .dialog-content-boxes .dialog-content-boxes-image p:nth-of-type(1){
  width: 90%;
  margin: 0 auto;
  font-size: 35rpx;
  display: flex;
  justify-content: space-between;
  line-height: 80rpx;
}
.dialog .dialog-content-boxes .dialog-content-boxes-image p:nth-of-type(1) span:nth-of-type(2){
  color:red;
}
.dialog .dialog-content-boxes .dialog-content-boxes-image p:nth-of-type(2){
  padding-left: 20rpx;
  width: 90%;
  margin: 0 auto;
  font-size: 25rpx;
  display: flex;
  flex-wrap: wrap;
  line-height: 50rpx;
}
.dialog .dialog-content-boxes .dialog-content-boxes-image p:nth-of-type(2) span:nth-of-type(1){
  flex:2;
  color:#9e9e9e;
}
.dialog .dialog-content-boxes .dialog-content-boxes-image p:nth-of-type(2) span:nth-of-type(2){
  flex:8;
  color:#000;
}
.dialog .dialog-content-boxes .dialog-content-boxes-image p:nth-of-type(3){
  padding-left: 20rpx;
  width: 90%;
  margin: 0 auto;
  font-size: 25rpx;
  display: flex;
  flex-wrap: wrap;
  line-height: 50rpx;
}
.dialog .dialog-content-boxes .dialog-content-boxes-image p:nth-of-type(3) span:nth-of-type(1){
  flex:2;
  color:#9e9e9e;
}
.dialog .dialog-content-boxes .dialog-content-boxes-image p:nth-of-type(3) span:nth-of-type(2){
  flex:8;
  color:#000;
}
.container{
  width:100%;
  height: 100%;
  background: #f7f7f7;
}
.container .container-detail{
  width: 100%;
  background: #fff;
}
.container .container-detail .container-detail-dl{
  width:90%;
  display: flex;
  margin:0 auto;
  padding:20rpx 0;
  border-bottom: 1px solid #ccc;
}
.container .container-detail .container-detail-dl .container-detail-dl-dt{
  margin-top: 20rpx;
  width:150rpx;
  height: 150rpx;
}
.container .container-detail .container-detail-dl .container-detail-dl-dt img{
  width:100%;
  height: 100%;
}
.container .container-detail .container-detail-dl .container-detail-dl-dd{
  flex:1;
  margin-left: 20rpx;
}
.container .container-detail .container-detail-dl .container-detail-dl-dd p:nth-of-type(1){
  width:100%;
  height: 60rpx;
  line-height: 60rpx;
  font-size: 32rpx;
}
.container .container-detail .container-detail-dl .container-detail-dl-dd p:nth-of-type(2){
  width:100%;
  height: 40rpx;
  line-height: 40rpx;
  font-size: 25rpx;
  font-size: 35rpx;
}
.container .container-detail .container-detail-dl .container-detail-dl-dd p:nth-of-type(2) span:nth-of-type(1){
  color:red;
  font-size: 25rpx;
  margin-right: 30rpx;
  margin-left: 20rpx;
}
.container .container-detail .container-detail-dl .container-detail-dl-dd p:nth-of-type(2) span:nth-of-type(2){
  color:skyblue;
  font-size: 25rpx;
}
.container .container-detail .container-detail-dl .container-detail-dl-dd p:nth-of-type(3){
  width:100%;
  height: 50rpx;
  line-height: 50rpx;
  font-size: 25rpx;
  color:#9e9e9e;
}
.container .container-detail .container-detail-dl .container-detail-dl-dd p:nth-of-type(4){
  width:100%;
  line-height: 30rpx;
  font-size: 25rpx;
  color:#9e9e9e;
}
.container .container-detail .container-detail-time{
  width:90%;
  margin: 0 auto;
  padding-bottom: 10rpx;
}
.container .container-detail .container-detail-time div:nth-of-type(1){
  width: 100%;
  display: flex;
  justify-content: space-between;
  color:#9e9e9e;
  line-height: 60rpx;
  font-size: 30rpx;
}
.container .container-detail .container-detail-time div:nth-of-type(1) span:nth-of-type(1),
.container .container-detail .container-detail-time div:nth-of-type(2) span:nth-of-type(1){
  flex:3.5;
  line-height: 60rpx;
}
.container .container-detail .container-detail-time div:nth-of-type(1) span:nth-of-type(2),
.container .container-detail .container-detail-time div:nth-of-type(2) span:nth-of-type(2){
  flex:3;
  text-align: center;
  font-size: 30rpx;
  color:red;
  line-height: 60rpx;
}
.container .container-detail .container-detail-time div:nth-of-type(1) span:nth-of-type(3),
.container .container-detail .container-detail-time div:nth-of-type(2) span:nth-of-type(3){
  flex:3.5;
  line-height: 60rpx;
}
.container .container-detail .container-detail-time div:nth-of-type(2){
  width: 100%;
  display: flex;
  justify-content: space-between;
}
.container .container-detail .container-detail-time div:nth-of-type(2) span:nth-of-type(1),
.container .container-detail .container-detail-time div:nth-of-type(2) span:nth-of-type(3){
  font-size: 32rpx;
}
.container .container-detail .container-detail-time div:nth-of-type(2) span:nth-of-type(1) span,
.container .container-detail .container-detail-time div:nth-of-type(2) span:nth-of-type(3) span{
  margin-left: 20rpx;
  font-size: 28rpx;
}
.container .container-detail-content{
  width:100%;
  margin-top: 30rpx;
}
.container .container-detail-content .container-detail-content-li{
  width:100%;
  background: #fff;
}
.container .container-detail-content .container-detail-content-li .container-detail-content-li-dl{
  width:90%;
  margin: 0 auto;
  display: flex;
  padding:20rpx 0;
}
.container .container-detail-content .container-detail-content-li .container-detail-content-li-dl .container-detail-content-li-dl-dt{
  width:120rpx;
  height: 120rpx;
}
.container .container-detail-content .container-detail-content-li .container-detail-content-li-dl .container-detail-content-li-dl-dt img{
  width: 100%;
  height: 100%;
}
.container .container-detail-content .container-detail-content-li .container-detail-content-li-dl .container-detail-content-li-dl-dd{
  margin-left: 20rpx;
  font-size: 30rpx;
}
.container .container-detail-content .container-detail-content-li .container-detail-content-li-dl .container-detail-content-li-dl-dd p:nth-of-type(1){
  width:100%;
  font-size: 30rpx;
  line-height: 50rpx;
}
.container .container-detail-content .container-detail-content-li .container-detail-content-li-dl .container-detail-content-li-dl-dd p:nth-of-type(2){
  width:100%;
  font-size: 25rpx;
  line-height: 40rpx;
  display: flex;
  color: #9e9e9e;
  justify-content: space-between;
}
.container .container-detail-content .container-detail-content-li .container-detail-content-li-dl .container-detail-content-li-dl-dd p:nth-of-type(2) span:nth-of-type(2){
  position: relative;
  right: -280rpx;
  top: 0;
}
.container .container-detail-content .container-detail-content-li .container-detail-content-li-dl .container-detail-content-li-dl-dd p:nth-of-type(2) span:nth-of-type(2) span{
  text-decoration:line-through
}
.container .container-detail-content .container-detail-content-li .container-detail-content-li-dl .container-detail-content-li-dl-dd p:nth-of-type(3){
  width:100%;
  color: #9e9e9e;
  font-size: 25rpx;
  line-height: 40rpx;
}
.container .container-detail-content .container-detail-content-li .container-detail-content-li-dl .container-detail-content-li-dl-dd p:nth-of-type(3) span{
  margin-right: 20rpx;
}
.container .container-detail-content .container-detail-content-li .container-detail-li-content{
  width:100%;
  background: #f7f7f7;
  line-height: 100rpx;
  height: 100rpx;
  display: flex;
  flex-wrap: wrap;
}
.container .container-detail-content .container-detail-content-li .container-detail-li-content span{
  font-size: 30rpx;
}
.container .container-detail-content .container-detail-content-li .container-detail-li-content span:nth-of-type(1){
  flex:6;
  margin-left: 20rpx;
}
.container .container-detail-content .container-detail-content-li .container-detail-li-content span:nth-of-type(2){
  flex:2;
  color:red;
  font-size: 22rpx;
}
.container .container-detail-content .container-detail-content-li .container-detail-li-content span:nth-of-type(3){
  flex:2;
  font-size: 25rpx;
}
.container .container-detail-content .container-detail-content-li .container-detail-li-content span:nth-of-type(3) span{
  background: #6dbdff;
  color:#fff;
  padding: 10rpx;

}
</style>
