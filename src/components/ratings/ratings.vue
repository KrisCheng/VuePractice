<template>
  <div class="ratings">
    <div class="ratings-content">
      <div class="overview">
        <div class="overview-left">
          <h1 class="score">{{seller.score}}</h1>
          <div class="title">综合评分</div>
          <div class="rank">高于周边商家{{seller.rankRate}}%</div>
        </div>
        <div class="overview-right"></div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default{
    props:{
      seller: {
        type: Object
      }
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/ratings.scss";
</style>
