<template>
  <div class="cartcontrol">
    <transition name="move">
    <div class="cart-decrease" v-show="food.count>0" @click.stop.prevent="decreaseCart">
      <span class="inner el-icon-minus"></span>
    </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add" @click.stop.prevent="addCart">
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
      addCart(event){
        if(!event._constructed){
          return;
        }
          if (!this.food.count) {
            Vue.set(this.food,'count',1);
          } else {
            this.food.count++;
          }
        this.$emit('add', event.target);
      },
      decreaseCart(){
        if(!event._constructed){
          return;
        }
        this.food.count--;
      }
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/cartcontrol.scss";
</style>
