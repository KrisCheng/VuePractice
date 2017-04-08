<template>
  <transition name="move">
  <div v-show="showFlag" class="food">
    <div class="food-content">
      <div class="image-header">
        <img :src="food.image">
      </div>
    </div>
  </div>
  </transition>
</template>

<script type="text/ecmascript-6">
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
      }
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/food.scss";
</style>
