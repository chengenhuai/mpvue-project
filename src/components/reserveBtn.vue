<template>
<div class='reserveBtn'>
    <button @click='navigateHotel'>预定酒店</button>
</div>
</template>

<script>
export default {
  methods: {
    navigateHotel () {
      wx.navigateTo({ url: '../hotel/main' })
    }
  }
}
</script>

<style>
.reserveBtn{
  width:100%;
  height:80rpx;
  line-height: 80rpx;
  margin:0 auto;
  padding: 60rpx 0;
  background: #fff;
}
.reserveBtn button{
  width:90%;
  margin:0 auto;
  background: #6dbdff;
  color:#fff;
}

</style>
