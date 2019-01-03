<template>
<div class="container">
  <div class="container-hotel-name">
    <img :src='hotel.picture'/>
  </div>
  <div class="container-hotel-detail">
    <p>{{hotel.name}}</p>
    <p>
      酒店详情: 美豪 取意"美丽中华 自豪国人" 致力做让所有宾客真正享有尊严的酒店 美豪大力推行会员忠诚度计划
      会员权益覆盖4+X个品牌 国内十个大中城市 近30家酒店 及真诚友好的个性化服务和丰富产品 折扣 积分 特权 惊喜 
      只为让您尊享更多 让旅行成为一种旅行方式
    </p>
  </div>
  <div class="container-hotel-tel">
    <p>电话: {{hotel.tel}}</p>
    <p>地址: {{hotel.address}}</p>
  </div>
  <div class="container-hotel-message">
    <p>
      <span>评分: {{hotel.commment.star}}分</span>
      <span>{{hotel.wechat_pay}}条评论</span>
    </p>
  </div>
  <div class="reserveBtn">
    <button>去订房</button>
  </div>
</div>
</template>

<script>
export default {
  data () {
    return {
      hotel: {
        picture: null,
        name: null,
        tel: null,
        address: null,
        wechat_pay: null,
        commment: {
          star: null
        }
      },
      data: 10,
      Tommrowdate: 10
    }
  },
  onLoad (e) {
    this.date = new Date().getDate()
    this.Tommrowdate = new Date().getDate() + 1
    this.month = new Date().getMonth() + 1
    if (this.date < 10) {
      this.date = '0' + this.date
    }
    if (this.Tommrowdate < 10) {
      this.Tommrowdate = '0' + this.Tommrowdate
    }
    if (this.month < 10) {
      this.month = '0' + this.month
    }
    wx.request({
      url: 'https://api.panguoyun.com/developers/wechat/gh_d38a1683ae09/type?start=2018-' + this.month + '-' + this.date + '&end=2018-' + this.month + '-' + this.Tommrowdate + '&id=' + parseInt(e.id),
      method: 'GET',
      dataType: 'json',
      success: (res) => {
        this.hotel = res.data.result.app
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
  width:100%;
  height: 100%;
  background: #f7f7f7;
}
.container-hotel-name{
  width:100%;
  height: 300rpx;
}
.container-hotel-name img{
  width:100%;
  height: 100%;
}
.container-hotel-detail{
  width:100%;
  background: #fff;
  padding-bottom: 20rpx;
}
.container-hotel-tel{
  margin-top: 30rpx;
  width:100%;
  background: #fff;
  padding:30rpx 0;
}
.container-hotel-tel p{
  width: 100%;
  padding-left: 30rpx;
  box-sizing: border-box;
  line-height: 40rpx;
  font-size: 25rpx;
}
.container-hotel-detail p:nth-of-type(1){
  width: 100%;
  line-height: 80rpx;
  height: 80rpx;
  font-size: 30rpx;
  padding-left: 30rpx;
  box-sizing: border-box;
}
.container-hotel-detail p:nth-of-type(2){
  width: 92%;
  margin: 0 auto;
  line-height: 40rpx;
  font-size: 25rpx;
  color:#9e9e9e;
}
.container-hotel-message{
  width: 100%;
  margin-top:30rpx;
  background: #fff;
}
.container-hotel-message p{
  width: 100%;
  padding-left: 30rpx;
  line-height: 80rpx;
  font-size: 25rpx;
  color:#9e9e9e;
  box-sizing: border-box;
  display: flex;
  justify-content: space-between;
}
.container-hotel-message p span:nth-of-type(2){
  margin-right: 30rpx;
}
.reserveBtn{
  position: fixed;
  width: 100%;
  height: 80rpx;
  line-height: 80rpx;
  bottom: 150rpx;
  left: 0;
}
.reserveBtn button{
  width: 90%;
  margin: 0 auto;
  height: 100%;
  font-size: 30rpx;
  text-align: center;
  color:#fff;
  background: #6dbdff;
}
</style>
