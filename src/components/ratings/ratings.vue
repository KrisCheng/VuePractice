<template>
  <div class="ratings" id="ratings">
    <div class="ratings-content">
      <div class="overview">
        <div class="overview-left">
          <h1 class="score">{{seller.score}}</h1>
          <div class="title">综合评分</div>
          <div class="rank">高于周边商家{{seller.rankRate}}%</div>
        </div>
        <div class="overview-right">
          <div class="score-wrapper">
            <span class="title">服务态度</span>
            <star :size="36" :score="seller.serviceScore"></star>
            <span class="score">{{seller.serviceScore}}</span>
          </div>
          <div class="score-wrapper">
            <span class="title">商品评分</span>
            <star :size="36" :score="seller.foodScore"></star>
            <span class="score">{{seller.foodScore}}</span>
          </div>
          <div class="delivery-wrapper">
            <span class="title">送达时间</span>
            <span class="delivery">{{seller.deliveryTime}}分钟</span>
          </div>
        </div>
      </div>
      <split></split>
      <ratingselect :select-type="selectType" @select="selectRating" @toggle="toggleContent" :only-content="onlyContent"  :ratings="ratings"></ratingselect>
      <div class="rating-wrapper">
        <ul v-show="ratings && ratings.length">
          <li v-show="needShow(rating.rateType,rating.text)" v-for="rating in ratings" class="rating-item">
            <div class="avatar">
              <img :src="rating.avatar" width="28" height="28">
            </div>
            <div class="content">
              <h1 class="name">{{rating.username}}</h1>
              <div class="star-wrapper">
                <star :size="24" :score="seller.foodScore"></star>
                <span class="delivery" v-show="rating.deliveryTime">{{rating.deliveryTime}}</span>
              </div>
              <p class="text">{{rating.text}}</p>
              <div class="recommend" v-show="rating.recommend && rating.recommend.length">
                <span class="fa fa-thumbs-up fa-lg"></span>
                <span class="item" v-for="item in rating.recommend">{{item}}</span>
              </div>
              <div class="time">
                {{rating.rateTime | formatDate}}
              </div>
            </div>
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
  import ratingselect from '../../components/ratingselect/ratingselect'
  import {formatDate} from '../../common/js/date'

  const ALL = 2;
  const ERR_OK = 0;

  export default{
    props:{
      seller: {
        type: Object
      }
    },
    created(){
      this.$http.get('/api/ratings').then((response) => {
        response = response.body;
        if(response.errno === ERR_OK){
          this.ratings = response.data;
          this.$nextTick(() => {
            this.scroll = new BScroll(document.getElementById('ratings'), {
              click: true
            });
          });
        }
      });
    },
    data(){
      return {
        ratings:[],
        selectType: ALL,
        onlyContent: true
      }
    },
    methods:{
      selectRating(type) {
        this.selectType = type;
        this.$nextTick(() => {
          this.scroll.refresh();
        });
      },
      toggleContent() {
        this.onlyContent = !this.onlyContent;
        this.$nextTick(() => {
          this.scroll.refresh();
        });
      },
      needShow(type,text){
        if(this.onlyContent && !text){
          return false;
        }
        if(this.selectType === ALL){
          return true;
        }
        else{
          return type === this.selectType;
        }
      }
    },
    filters:{
      formatDate(time){
        let date = new Date(time);
        return formatDate(date,'yyyy-MM-dd hh:mm');
      }
    },
    components: {
      star,
      ratingselect,
      split
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/ratings.scss";
  @import "../../../static/css/font-awesome.min.css";
</style>
