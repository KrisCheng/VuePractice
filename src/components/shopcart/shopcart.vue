<template>
  <div class="shopcart">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo">
            <span class="el-icon-menu"></span>
          </div>
        </div>
        <div class="price">${{totalPrice}}</div>
        <div class="desc">另需配送费${{deliveryPrice}}</div>
      </div>
      <div class="content-right">
        <div class="pay">
          ${{minPrice}}起送
        </div>
      </div>
    </div>
  </div>

</template>

<script type="text/ecmascript-6">
  export default{
    props:{
      selectFoods:{
        type: Array,
        default(){
          return [];
        }
      },
      deliveryPrice:{
        type: Number,
        default: 0
      },
      minPrice:{
        type: Number,
        default: 0
      }
    },
    computed:{
      totalPrice(){
        let total = 0;
        this.selectFoods.forEach((food) => {
          total += food.price * food.count;
        });
        return total;
      },
      totalCount(){
        let count = 0;
        this.selectFoods.forEach((food) => {
          count += food.count;
        });
        return count;
      }
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/shopcart.scss";
</style>
