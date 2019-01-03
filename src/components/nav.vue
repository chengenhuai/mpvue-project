<template>
<div class='nav'>
  <div class='nav-li' @click='navgateTo'>
    <div><img src='../images/site.png'/>所在城市</div>
    <div>{{content}}</div>
    <div><img src='../images/Right.png'/></div>
  </div>
  <div class='nav-li'>
    <div @click="skipCalendar"><img src='../images/date.png'/>入住日期</div>
    <div>
      <picker mode="date" @change="bindPickerChange" :value="time" :start="startTime" end="2099-12-31">
        <div class="picker">
          {{time}}晚
        </div>
      </picker>
    </div>
    <div><img src='../images/Right.png'/></div>
  </div>
  <div class='nav-li'>
    <div><img src='../images/hotel.png'/><input placeholder='请输入酒店名/关键字' @input='changeCity'></input></div>
    <div></div>
    <div><img src='../images/Right.png'/></div>
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
  props: ['content', 'time'],
  methods: {
    bindPickerChange (e) {
      let changeTime = e.target.value
      let changeTimeMonth = changeTime.split('-')[1]
      let changeTimeDate = changeTime.split('-')[2]
      this.time = changeTimeMonth + '月' + changeTimeDate + '日'
    },
    navgateTo () {
      wx.navigateTo({ url: '../city/main' })
    },
    changeCity (e) {
      wx.setStorageSync('key', e.target.value)
    },
    skipCalendar () {
      wx.navigateTo({ url: '../calendar/main' })
    }
  }
}
</script>

<style>
.nav{
  width:100%;
  background: #fff;
}
.nav .nav-li{
  width:90%;
  margin:0 auto;
  border-bottom:1px solid #ccc;
  display: flex;
  flex-wrap: wrap;
  padding:30rpx 0;
}
.nav .nav-li:nth-of-type(3){
  padding:25rpx 0;
}
.nav .nav-li:nth-of-type(3) div:nth-of-type(1){
  flex:9;
  display: flex;
}
.nav .nav-li:nth-of-type(3) div:nth-of-type(1) img{
  display: inline-block;
  width:40rpx;
  height: 40rpx;
  margin-top: 5rpx;
}
.nav .nav-li:nth-of-type(3) div:nth-of-type(1) input{
  width:100%;
}
.nav .nav-li:nth-of-type(3) div:nth-of-type(2){
  flex:0;
}
.nav .nav-li:nth-of-type(3) div:nth-of-type(3){
  flex:1;
}
.nav .nav-li div{
  font-size: 30rpx;
  font-weight: 550;
}
.nav .nav-li div:nth-of-type(1){
  flex:4;
}
.nav .nav-li div:nth-of-type(1) img{
  width:30rpx;
  height:30rpx;
  margin-right:20rpx;
}
.nav .nav-li div:nth-of-type(2){
  flex:5;
  text-align: right;
}
.nav .nav-li div:nth-of-type(3){
  flex:1;
}
.nav .nav-li div:nth-of-type(3) img{
  display: inline-block;
  width:30rpx;
  height:30rpx;
  margin-right:20rpx;
  position: relative;
  top:4rpx;
  right:-20rpx;
}
</style>
