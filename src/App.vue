<template>
  <div id="app">
    <v-header></v-header>
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

<script>
  import header from './components/header/header.vue'
  import goods from './components/goods/goods.vue'
  export default {
    components: {
      'v-header': header,
      'goods': goods
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
 @import "../static/css/App.scss";
</style>
