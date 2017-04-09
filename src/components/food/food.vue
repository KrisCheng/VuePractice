<template>
  <transition name="move">
  <div v-show="showFlag" class="food" id="food">
    <div class="food-content">
      <div class="image-header">
        <img :src="food.image">
        <div class="back">
          <i class="el-icon-arrow-left" @click="hide"></i>
        </div>
      </div>
      <div class="content">
        <h1 class="title">{{food.name}}</h1>
        <div class="detail">
          <span class="sell-count">月售{{food.sellCount}}份</span>
          <span class="rating">好评率{{food.rating}}%</span>
        </div>
        <div class="price">
          <span class="now"><span class="tag">$</span>{{food.price}}</span>
          <span class="old" v-show="food.oldPrice">${{food.oldPrice}}</span>
        </div>
      <div class="cartcontrol-wrapper">
        <cartcontrol :food="food"></cartcontrol>
      </div>
      <transition name="add">
      <div @click.stop.prevent="addFirst" class="buy" v-show="!food.count || food.count===0">
        加入购物车
      </div>
      </transition>
    </div>
    <split v-show="food.info"></split>
    <div class="info" v-show="food.info">
      <h1 class="title">商品介绍</h1>
      <p class="text">{{food.info}}</p>
    </div>
  </div>
  </div>
  </transition>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll'
  import Vue from 'vue'
  import cartcontrol from '../../components/cartcontrol/cartcontrol'
  import split from '../../components/split/split'

  export default {
    props:{
      food:{
        type: Object
      }
    },
    data(){
      return{
        showFlag: false
      };
    },
    methods:{
      show(){
        this.showFlag = true;
        this.$nextTick(() => {
          if(!this.scroll){
            this.scroll = new BScroll(document.getElementById('food'),{
              click: true
            });
          }
        });
      },
      hide(){
        this.showFlag = false;
      },
      addFirst(event){
        if(!event._constructed){
          return;
        }
        Vue.set(this.food,'count',1);
      }
    },
    components:{
      cartcontrol,
      split
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/food.scss";
</style>
