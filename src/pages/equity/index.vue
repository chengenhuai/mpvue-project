<template>
  <div class="container">
    <swiper indicator-dots='true' class="container-equity" @change="bindChange">
        <block v-for='item in banner' :key='index'>
            <swiper-item class="container-equity-img">
              <div>{{item.name}}</div>
              <div>{{item.content}}</div>
            </swiper-item>
        </block>
    </swiper>
    <div class="container-content">
      <div class="container-content-h5">
        会员权益
      </div>
      <div :class="name">
        <img :src="img"/>
      </div>
    </div>
    <div class="container-rules">
      <div class="container-rules-h5">
        积分规则
      </div>
      <div class="container-rules-point">
        <div>1: 积分方式: 住房1元积1分 用餐4元积一分</div>
        <div>2: 兑换方式: 积分可以到酒店前台兑换响应的礼品 积分可以到酒店前台兑换房费</div>
        <div>3: 兑换标准: 40个积分可以兑换1元房费 1000个积分起兑</div>
        <div>4:（黄金卡 铂金卡 至尊卡住房享受同等折扣）</div>
      </div>
    </div>
    <div class="container-rules">
      <div class="container-rules-h5">
        会员升级
      </div>
      <div class="container-rules-point">
        <div class="container-rules-point-line">普卡会员</div>
        <div>通过关注美豪集团微信公众号 (注册即送900元大礼包)</div>
        <div>通过美豪集团官网免费注册 (注册即送900元大礼包)</div>
        <div>延时退房至15:00点</div>
        <div class="container-rules-point-line">黄金卡</div>
        <div>累计入住15个间夜 免费升级为黄金卡 (扣除响应积分) 延时退房至16:00点</div>
        <div class="container-rules-point-line">铂金卡会员</div>
        <div>累计入住50个间夜免费升级为铂金卡 延时退房至17:00点</div>
        <div class="container-rules-point-line">至尊卡会员</div>
        <div>美豪业主 美豪特殊合作伙伴 美豪特殊客户 延时退房至18:00点</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      banner: [{
        name: '普通会员',
        content: '会员等级'
      }, {
        name: '金卡会员',
        content: '会员等级'
      }, {
        name: '铂金卡会员',
        content: '会员等级'
      }, {
        name: '钻石卡会员',
        content: '会员等级'
      }],
      img: '/static/equity_01.png',
      name: 'container-content-point'
    }
  },
  methods: {
    bindChange (e) {
      if (e.mp.detail.current > 1) {
        this.img = '/static/equity_02.png'
        this.name = 'container-content-img'
      } else {
        this.img = '/static/equity_01.png'
        this.name = 'container-content-point'
      }
    }
  }
}
</script>

<style>
.container{
  width: 100%;
  height: 100%;
  background: #f7f7f7;
}
.container .container-equity{
  width:100%;
  height: 250rpx;
}
.container .container-equity .container-equity-img{
  width: 100%;
  height: 100%;
  color:#fff;
}
.container .container-equity .container-equity-img div:nth-of-type(1){
  width:100%;
  height: 100rpx;
  text-align: center;
  font-size: 35rpx;
  line-height: 100rpx;
}
.container .container-equity .container-equity-img div:nth-of-type(2){
  width:100%;
  height: 60rpx;
  line-height: 60rpx;
  text-align: center;
  font-size: 25rpx;
}
.container .container-equity .container-equity-img:nth-of-type(1){
  background: skyblue;
}
.container .container-equity .container-equity-img:nth-of-type(2){
  background: brown;
}
.container .container-equity .container-equity-img:nth-of-type(3){
  background: #ccc;
}
.container .container-equity .container-equity-img:nth-of-type(4){
  background: pink;
}
.container .container-content{
  width:100%;
  margin-top: 40rpx;
  background: #fff;
}
.container .container-content .container-content-h5{
  width:90%;
  margin:0 auto;
  height: 80rpx;
  font-size: 35rpx;
  line-height: 80rpx;
  text-align: center;
  border-bottom: 1px solid #ccc;
}
.container .container-content .container-content-point{
  width:100%;
  height: 320rpx;
}
.container .container-content .container-content-img{
  width: 100%;
  height: 450rpx;
}
.container .container-content .container-content-img img{
  width: 100%;
  height: 100%;
}
.container .container-content .container-content-point img{
  width: 100%;
  height: 100%;
}
.container .container-rules{
  width:100%;
  background: #fff;
  margin-top: 40rpx;
}
.container .container-rules .container-rules-h5{
  width:90%;
  margin:0 auto;
  font-size: 35rpx;
  height: 80rpx;
  line-height: 80rpx;
  text-align: center;
  border-bottom: 1px solid #ccc;
}
.container .container-rules .container-rules-point{
  width: 90%;
  margin: 0 auto;
  padding: 20rpx 0;
}
.container .container-rules .container-rules-point div{
  width: 100%;
  font-size: 25rpx;
  line-height: 40rpx;
}
.container .container-rules .container-rules-point .container-rules-point-line{
  line-height: 60rpx;
}
</style>
