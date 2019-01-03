<template>
<div class='banner'>
  <swiper indicator-dots='true' autoplay='true' indicator-color='#fff' indicator-active-color='#6bc4ff' circular='true'>
      <block v-for="item in banner" :key="index">
          <swiper-item :data-id='item.path' @click='skipDetail'>
              <img :src="item.pic"></img>
          </swiper-item>
      </block>
  </swiper>
</div>
</template>

<script>
export default {
  props: ['banner'],
  methods: {
    skipDetail (e) {
      var url = '../detail/main?id=' + e.currentTarget.dataset.id
      wx.navigateTo({ url })
    }
  }
}
</script>

<style>
.banner{
  width:100%;
  height:300rpx;
  background: #fff;
}
.banner swiper{
  width:100%;
}
.banner swiper swiper-item{
  width:100%;
}
.banner swiper swiper-item img{
  width:100%;
  height:100%;
}

</style>

