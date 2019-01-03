<template>
<div class="container">
  <div class="container-user-form">
    <div class="container-user-form-photo">
      <span>手机号</span>
      <input type="text" placeholder="输入手机号" :value='userName' @input='changeUser'>
    </div>
    <div class="container-user-form-password">
      <span>密码</span>
      <input type="password" placeholder="输入密码" :value='passWord' @input='changePass'>
      <span>忘记密码</span>
    </div>
  </div>
  <div class="container-user-content">
    如果没有账号密码点击<span>注册.</span>
  </div>
  <div :hidden='Isshow' class="container-warn">
    您所输入的账号或密码不正确
  </div>
  <div class="container-user-button">
    <button @click='bound'>绑定</button>
  </div>
</div>
</template>

<script>
export default {
  data () {
    return {
      userName: null,
      passWord: null,
      defaultUser: 13718319642,
      defaultPass: 13152985728,
      Isshow: true
    }
  },
  methods: {
    bound () {
      if (parseInt(this.defaultUser) === parseInt(this.userName) && parseInt(this.defaultPass) === parseInt(this.passWord)) {
        this.Isshow = true
        wx.setStorageSync('login', true)
        wx.redirectTo({ url: '../home/main' })
      } else {
        this.Isshow = false
      }
    },
    changeUser (e) {
      this.userName = e.target.value
    },
    changePass (e) {
      this.passWord = e.target.value
    }
  }
}
</script>

<style>
.container{
  background: #f7f7f7;
}
.container .container-user-form{
  width:100%;
  margin-top: 20rpx;
  background: #fff;
}
.container .container-user-form .container-user-form-photo{
  width:100%;
  height: 100rpx;
  line-height: 100rpx;
  display: flex;
  border-bottom: 1px solid #ccc;
  font-size: 30rpx;
}
.container .container-user-form .container-user-form-photo span{
  flex:2;
  text-align: center;
}
.container .container-user-form .container-user-form-photo input{
  flex:8;
  width:100%;
  height:40rpx;
  margin-top: 25rpx;
  padding-left: 20rpx;
  box-sizing: border-box;
  font-size: 30rpx;
}
.container .container-user-form .container-user-form-password{
  display: flex;
  width:100%;
  height: 100rpx;
  line-height: 100rpx;
  font-size: 30rpx;
}
.container .container-user-form .container-user-form-password span:nth-of-type(1){
  flex:2;
  text-align: center;
}
.container .container-user-form .container-user-form-password input{
  flex:5;
  width:100%;
  height:40rpx;
  margin-top: 25rpx;
  padding-left: 20rpx;
  box-sizing: border-box;
  font-size: 30rpx;
}
.container .container-user-form .container-user-form-password span:nth-of-type(2){
  flex:3;
  text-align: center;
  border-left: 1px solid #ccc;
}
.container .container-user-content{
  width: 100%;
  height: 80rpx;
  line-height: 80rpx;
  padding-left: 30rpx;
  box-sizing: border-box;
  font-size: 30rpx;
}
.container .container-user-content span{
  color:red;
}
.container .container-user-button{
  width:100%;
  margin-top: 650rpx;
}
.container .container-user-button button{
  width:90%;
  height: 80rpx;
  line-height: 80rpx;
  text-align: center;
  font-size: 30rpx;
  background: #6ebbff;
  color:#fff;
  position: fixed;
  bottom: 100rpx;
  left: 5%;
}
.container .container-warn{
  width: 100%;
  height: 80rpx;
  line-height: 80rpx;
  padding-left: 30rpx;
  box-sizing: border-box;
  font-size: 30rpx;
  color:red;
}
</style>

