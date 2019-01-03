<script>
export default {
  created () {},
  onUnload () {
    wx.clearStorageSync()
  }
}
</script>

<style>
Page{
  width:100%;
  height:100%;
}
.container{
  width:100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}
.container .section{
  flex:1;
  width:100%;
}
/* this rule will be remove */
* {
  transition: width 2s;
  -moz-transition: width 2s;
  -webkit-transition: width 2s;
  -o-transition: width 2s;
}
</style>
