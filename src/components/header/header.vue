<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" src="./chaofen.jpeg">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="el-icon-arrow-right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="el-icon-arrow-right"></i>
    </div>
    <div class="background">
      <img src="./chaofen.jpeg" width="100%" height="100%">
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default{
    props: {
      seller: {
        type: Object
      }
    },
    created () {
      this.classMap = ['decrease', 'discount', 'invoice', 'guarantee']
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
@import "../../../static/css/header.scss";
</style>
