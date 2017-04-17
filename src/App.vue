
<template>
  <div>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods" class="item">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings" class="item">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller" class="item">商家</router-link>
      </div>
    </div>
    <keep-alive>
    <router-view :seller="seller"></router-view>
    </keep-alive>
  </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import {urlParse} from './common/js/util'
  import header from './components/header/header.vue'
  import goods from './components/goods/goods.vue'
  const ERR_OK = 0;
  export default {
    components: {
      'v-header': header
    },

    data () {
      return {
        seller: {
          id: (() =>{
            let queryParam = urlParse();
            return queryParam.id;
          })()
        }
      }
    },
    created () {
      this.$http.get('/api/seller?id='+this.seller.id).then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.seller = response.data;
        }
      })
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
 @import "../static/css/App.scss";
</style>
