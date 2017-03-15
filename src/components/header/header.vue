<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
    </div>

    <div class="bulletin-wrapper">
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default{
    props: {
      seller: {
        type: Object
      }
    },
    created () {
      this.classMap = ['decrease', 'discount', 'invoice', 'guarantee']
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
.header{
  color: #fff;
  background-color: black;
  .content-wrapper{
    padding: 24px 12px 18px 24px;
    font-size: 0px;
    .avatar{
      font-size:14px;
      display: inline-block;
      img{
        border-radius: 2px;
      }
    }
    .content{
      font-size: 14px;
      display: inline-block;
      margin-left: 14px;
      .title{
        margin: 2px 0 8px 0;
        .brand{
          display: inline-block;
          vertical-align: text-top;
          width: 30px;
          height: 18px;
          background-image: url("./brand@2x.png");
          background-size: 30px 18px;
        }
        .name{
          margin-left: 6px;
          font-size: 16px;
          line-height: 18px;
          font-weight: bold;
        }
      }
      .description {
        margin-bottom: 10px;
        line-height: 12px;
        font-size: 12px;
      }
      .support {
        .icon {
          display: inline-block;
          vertical-align: text-top;
          width: 12px;
          height: 12px;
          margin-right: 4px;
          background-size: 12px 12px;
          background-repeat: no-repeat;
          background-image: url("./decrease_1@2x.png");
        }
        .text {
          line-height: 12px;
          font-size: 12px;
        }
      }
    }
  }
}
</style>
