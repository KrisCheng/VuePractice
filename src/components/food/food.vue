<template>
  <div v-show="showFlag" class="food">

  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props:{
      food:{
        type:Object
      }
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/food.scss";
</style>
