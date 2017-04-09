<template>
  <div class="ratingselect">
    <div class="rating-type">
      <span @click="select(2,$event)" class="block positive" :class="{'active':selectType===2}">{{desc.all}}<span class="count">{{ratings.length}}</span></span>
      <span @click="select(0,$event)" class="block positive" :class="{'active':selectType===0}">{{desc.positive}}<span class="count">{{positives.length}}</span></span>
      <span @click="select(1,$event)" class="block negative" :class="{'active':selectType===1}">{{desc.negative}}<span class="count">{{negatives.length}}</span></span>
    </div>
    <div @click="toggleContent($event)" class="switch" :class="{'on':onlyContent}">
      <span class="el-icon-circle-check"></span>
      <span class="text">只查看有内容的评价</span>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  const POSITIVE = 0;
  const NEGATIVE = 1;
  const ALL = 2;
  export default{
    props: {
      ratings: {
        type: Array,
        default(){
          return [];
        }
      },
      selectType: {
        type: Number,
        default: 1
      },
      onlyContent: {
        type: Boolean,
        default: false
      },
      desc: {
        type: Object,
        default() {
          return {
            all: '全部',
            positive: '满意',
            negative: '不满意'
          };
        }
      }
    },
    computed:{
      positives(){
        return this.ratings.filter((rating)=> {
          return rating.rateType === POSITIVE;
        });
      },
      negatives(){
        return this.ratings.filter((rating)=> {
          return rating.rateType === NEGATIVE;
        });
      }
    },
    methods:{
      select(type,event){
        if(!event._constructed){
          return;
        }
        this.selectType = type;
        this.$emit('ratingtype.select', type);
      },
      toggleContent(event){
        if(!event._constructed){
          return;
        }
        this.onlyContent = !this.onlyContent;
        this.$emit('ratingtype.select', this.onlyContent);
      }
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../../static/css/ratingselect.scss";
</style>
