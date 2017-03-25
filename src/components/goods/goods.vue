<template>
  <div class="goods">
    <div class="menu-wrapper"></div>
    <div class="foods-wrapper"></div>

  </div>
</template>

<script type="text/ecmascript-6">
  const ERR_OK = 0;
  export default{
    props:{
      seller:{
        type: Object
      }
    },
    data(){
      return {
        goods: []
      }
    },
    created(){
      this.$http.get('/api/goods').then((response) => {
        response = response.body;
        if(response.errno === ERR_OK){
          this.goods = response.data;
          console.log(this.goods);
        }
      })
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/goods.scss";
</style>
