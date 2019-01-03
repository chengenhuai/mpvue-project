<template>
<div class='container'>
  <div class='banner'>
    <img src="../../images/homepage.png"></img>
  </div>
  <div class='loginButton'>
    <button @click='navigateTo'>登录</button>
  </div>
</div>
</template>

<script>
export default {
  data () {
    return {}
  },
  onShow () {
    let getLocal = wx.getStorageSync('state')
    if (getLocal) {
      wx.navigateTo({ url: '../home/main' })
    }
  },
  methods: {
    navigateTo () {
      wx.setStorageSync('state', true)
      wx.navigateTo({ url: '../home/main' })
    }
  }
}
</script>

<style scoped>
.banner{
  width:100%;
  height:300rpx;
  margin-top: 200rpx;
}
.banner img{
  display: block;
  width:55%;
  height:100%;
  margin:0 auto;
}
.loginButton{
  width:90%;
  height:80rpx;
  line-height: 80rpx;
  margin:0 auto;
  margin-top: 300rpx;
  cursor:pointer
}
.loginButton button{
  font-size: 30rpx;
  width: 100%;
  height:100%;
  background: #6ebbff;
  color:#fff;
}
</style>
