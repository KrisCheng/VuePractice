<template>
  <div class="goods">
    <div class="menu-wrapper" id="menu-wrapper">
    <ul>
      <li v-for="item in goods" class="menu-item">
        <span class="text">
          <span v-show="item.type>0" class="icon"></span>
          {{item.name}}
        </span>
      </li>
    </ul>
    </div>
    <div class="foods-wrapper" id="foods-wrapper">
      <ul>
        <li v-for="item in goods" class="food-list">
          <h1 class="title">{{item.name}}</h1>
        <ul>
          <li v-for="food in item.foods" class="food-items">
            <div class="icon">
            <img  width="57px" height="57px" :src="food.icon">
            </div>
            <div class="content">
              <h2 class="name">{{food.name}}</h2>
              <p class="desc">{{food.description}}</p>
              <div class="extra">
                <span class="count">月售{{food.sellCount}}份</span>
                <span>好评率{{food.rating}}%</span>
              </div>
              <div class="price">
                <span class="now">${{food.price}}</span>
                <span class="old" v-show="food.oldPrice">${{food.oldPrice}}</span>
              </div>
            </div>
          </li>
        </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll';
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
          this.$nextTick(() => {
            this._initScroll();
          });
        }
      })
    },
    methods: {
      _initScroll() {
        this.menuScroll = new BScroll(document.getElementById('menu-wrapper'));
        this.foodsScroll = new BScroll(document.getElementById('foods-wrapper'));
      }
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/goods.scss";
</style>
