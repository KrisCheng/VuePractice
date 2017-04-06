<template>
  <div class="cartcontrol">
    <div class="cart-decrease" v-show="food.count>0" @click="decreaseCart" transition="move">
      <span class="el-icon-minus"></span>
    </div>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add" @click="addCart">
      <span class="el-icon-plus"></span>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue';
  export default{
    props:{
      food:{
        type: Object
      }
    },
    methods:{
      addCart(){
          if (!this.food.count) {
            Vue.set(this.food,'count',1);
          } else {
            this.food.count++;
          }
      },
      decreaseCart(){
        this.food.count--;
      }
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/cartcontrol.scss";
</style>
