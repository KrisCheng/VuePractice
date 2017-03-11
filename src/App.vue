<template>
  <div id="app">
    <v-header></v-header>
    <div class="tab">
      <div class="tab-item">商品</div>
      <div class="tab-item">评论</div>
      <div class="tab-item">商家</div>
    </div>
    <div class="content">
      这是内容页
    </div>
  </div>
</template>

<script>
  import header from './components/header/header.vue'

  export default {
    components: {
      'v-header': header
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
  .tab {
    display: flex;
    width: 100%;
    height: 40px;
    line-height: 40px;
  .tab-item {
    flex: 1;
    text-align: center;
  }
  }
</style>
