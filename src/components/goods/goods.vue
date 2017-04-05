<template>
  <div class="goods">
    <div class="menu-wrapper" id="menu-wrapper">
    <ul>
      <li v-for="(item,$index,$event) in goods" class="menu-item"  :class="{'current':currentIndex===$index}"
          @click="selectMenu($index,$event)">
        <span class="text">
          <span v-show="item.type>0" class="icon"></span>
          {{item.name}}
        </span>
      </li>
    </ul>
    </div>
    <div class="foods-wrapper" id="foods-wrapper">
      <ul>
        <li v-for="item in goods" class="food-list food-list-hook">
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
    <shopcart :delivery-price="seller.deliveryPrice" :min-price="seller.minPrice"></shopcart>
  </div>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll';
  import shopcart from '../../components/shopcart/shopcart'

  const ERR_OK = 0;
  export default{
    props:{
      seller:{
        type: Object
      }
    },
    data(){
      return {
        goods: [],
        listHeight: [],
        scrollY: 0
      }
    },
    computed: {
      currentIndex() {
        for(let i=0; i<this.listHeight.length; i++){
          let height1 = this.listHeight[i];
          let height2 = this.listHeight[i+1];
          if(!height2 || (this.scrollY >= height1 && this.scrollY < height2)){
            return i;
          }
        }
        return 0;
      },
      selectFoods() {
        let foods = [];
        this.goods.forEach((good) => {
          good.foods.forEach((food) => {
            if (food.count) {
              foods.push(food);
            }
          });
        });
        return foods;
      }
    },
    created(){
      this.$http.get('/api/goods').then((response) => {
        response = response.body;
        if(response.errno === ERR_OK){
          this.goods = response.data;
          this.$nextTick(() => {
            this._initScroll();
            this._calculateHeight();
          });
        }
      })
    },
    methods: {
      selectMenu(index, event) {
        if (!event._constructed) {
          return;
        }
        let foodList = document.getElementById('foods-wrapper').getElementsByClassName('food-list-hook');
        let el = foodList[index];
        this.foodsScroll.scrollToElement(el, 300);
      },
      _initScroll() {
        this.menuScroll = new BScroll(document.getElementById('menu-wrapper'),{
          click: true
        });
        this.foodsScroll = new BScroll(document.getElementById('foods-wrapper'),{
          click: true,
          probeType: 3
        });
        this.foodsScroll.on('scroll', (pos) => {
          this.scrollY = Math.abs(Math.round(pos.y));
        })
      },
      _calculateHeight() {
        let foodsList = document.getElementById('foods-wrapper').getElementsByClassName('food-list-hook');
        let height = 0;
        this.listHeight.push(height);
        for(let i=0; i<foodsList.length; i++){
          let item = foodsList[i];
          height += item.clientHeight;
          this.listHeight.push(height);
        }
      }
    },
    components: {
      shopcart
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/goods.scss";
</style>
