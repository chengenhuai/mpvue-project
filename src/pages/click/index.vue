<template>
<div class="container">
  <div v-for='(item, index) in Json' v-text='item.name' :key='index' @click='Title_first(item, item.id)'>
    <div v-for='(value, key) in renderData_01' :key='value.id' v-text='value.name' v-if='activeIndex_01 == index' @click='Title_Two(value, value.id)'>
      <div v-for='(data, info) in renderData_02' :key='info' v-text='data.name' v-if='activeIndex_02 == value.id'></div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  data () {
    return {
      renderData_01: null,
      renderData_02: null,
      activeIndex_01: null,
      activeIndex_02: null,
      Json: null
    }
  },
  onLoad () {
    wx.request({
      url: 'https://easy-mock.com/mock/5b61a0332205a5414ac525da/example/title',
      method: 'get',
      success: (res) => {
        this.Json = res.data.data
        console.log(res.data.data)
      }
    })
  },
  methods: {
    Title_first (e, eId) {
      this.renderData_01 = e.content
      this.activeIndex_01 = eId
    },
    Title_Two (e, eId) {
      this.renderData_02 = e.content
      this.activeIndex_02 = eId
      console.log(e, eId)
    }
  }
}
</script>

<style>

</style>
