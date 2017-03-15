<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods" class="item">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings" class="item">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller" class="item">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
    <div class="content">
      这是内容
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header.vue'
  import goods from './components/goods/goods.vue'
  const ERR_OK = 0
  export default {
    components: {
      'v-header': header,
      'goods': goods
    },

    data () {
      return {
        seller: {}
      }
    },
    created () {
      this.$http.get('/api/seller').then((response) => {
        response = response.body
        if (response.errno === ERR_OK) {
          this.seller = response.data
          console.log(this.seller)
        }
      })
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
 @import "../static/css/App.scss";
</style>
