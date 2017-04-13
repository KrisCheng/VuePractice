<template>
  <div class="seller" id="seller">
    <div class="seller-content">
      <div class="overview">
        <h1 class="title">{{seller.name}}</h1>
        <div class="desc">
          <star :size="36" :score="seller.score"></star>
          <span class="text">({{seller.ratingCount}})</span>
          <span class="text">月售{{seller.sellCount}}单</span>
        </div>
        <ul class="remark">
          <li class="block">
            <h2>起送价</h2>
            <div class="content">
              <span class="stress">{{seller.minPrice}}</span>元
            </div>
          </li>
          <li class="block">
            <h2>商家配送</h2>
            <div class="content">
              <span class="stress">{{seller.deliveryPrice}}</span>元
            </div>
          </li>
          <li class="block">
            <h2>平均配送时间</h2>
            <div class="content">
              <span class="stress">{{seller.deliveryTime}}</span>分钟
            </div>
          </li>
        </ul>
      </div>
      <split></split>
      <div class="bulletin">
        <h1 class="title">公告与活动</h1>
        <div class="content-wrapper">
          <div class="content">
            {{seller.bulletin}}
          </div>
        </div>
        <ul v-if="seller.supports" class="supports">
          <li class="support-item" v-for="(item,index) in seller.supports">
            <span class="icon"></span>
            <span class="text">{{seller.supports[index].description}}</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll'
  import star from '../../components/star/star'
  import split from '../../components/split/split'

  export default{
    props:{
      seller:{
        type:Object
      }
    },
    watch:{
      'seller'(){
        this.$nextTick(() => {
          this._initScroll();
        });
      }
    },
    methods:{
      _initScroll(){
        if(!this.scroll){
          this.scroll = new BScroll(document.getElementById('seller'),{
            click: true
          });
        }else {
          this.scroll.refresh();
        }
      }
    },
    components: {
      star,
      split
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/seller.scss";
</style>
