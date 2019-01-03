<template>
<div class="container">
  <div class='section'>
    <Banners :banner='banner'></Banners>
    <Navs :content='content' :time='time'></Navs>
    <ReserveBtn></ReserveBtn>
    <userEquity></userEquity>
    <Bottom></Bottom>
  </div>
  <div class="footer">
    <dl>
      <dt>
        <img src="../../images/reserve_02.png" alt="">
      </dt>
      <dd>预定</dd>
    </dl>
    <dl @click='skipIndex'>
      <dt>
        <img src="../../images/icon_02.png" alt="">
      </dt>
      <dd>我的</dd>
    </dl>
  </div>
</div>
</template>

<script>
import userEquity from '../../components/userEquity'
import Bottom from '../../components/bottom'
import ReserveBtn from '../../components/reserveBtn'
import Navs from '../../components/nav'
import Banners from '../../components/banner'

export default {
  data () {
    return {
      banner: [],
      time: null,
      content: '不限'
    }
  },
  components: {
    userEquity,
    Bottom,
    ReserveBtn,
    Navs,
    Banners
  },
  onShow () {
    let localContent = wx.getStorageSync('value')
    if (localContent.length !== 0) {
      this.content = localContent
    }
  },
  onLoad () {
    wx.showLoading()
    let timeMonth = new Date().getMonth() + 1
    let timeDate = new Date().getDate()
    if (timeMonth < 10) {
      timeMonth = '0' + timeMonth
    }
    this.time = timeMonth + '月' + timeDate + '日'
    // 列表的banner
    wx.request({
      url: 'https://api.panguoyun.com/developers/wechat/gh_d38a1683ae09/app/banner',
      method: 'GET',
      dataType: 'json',
      success: (res) => {
        res.data.result.map((item, index) => {
          item.path = item.path.split('=')[1]
        })
        this.banner = res.data.result
      },
      fail: () => {},
      complete: () => {
        wx.hideLoading()
      }
    })
  },
  methods: {
    skipIndex () {
      wx.navigateTo({ url: '../user/main' })
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
.container .section{
  flex:1;
  width:100%;
  background: #f7f7f7;
  padding-bottom:120rpx;
}
.container .footer{
  position: fixed;
  bottom:0;
  left:0;
  width:100%;
  height:120rpx;
  display: flex;
  background: #fff;
  border-top:1px solid #ccc;
}
.container .footer dl{
  flex:1;
}
.container .footer dl dt{
  width:50rpx;
  height:50rpx;
  margin:10rpx auto;
}
.container .footer dl dt img{
  width:100%;
  height:100%;
}
.container .footer dl dd{
  text-align: center;
  width: 100%;
  font-size: 30rpx;
}
</style>
