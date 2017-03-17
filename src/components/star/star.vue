<template>
  <div class="star star-48">
    sss
    <span v-for="itemClass in itemClasses" class="star-item" :class="itemClass" track-by="$index">
      111
    </span>
  </div>
</template>

<script type="text/ecmascript-6">
  const LENGTH = 5
  const CLS_ON = 'on'
  const CLS_HALF = 'half'
  const CLS_OFF = 'off'

  export default {
    props: {
      size: {
        type: Number
      },
      score: {
        type: Number
      }
    },
    computed: {
      starType () {
        return 'star-' + this.size
      },
      itemClasses () {
        let result = []
        let score = Math.floor(this.score*2) / 2
        let hasDecimal = score%1 !== 0
        let integer = Math.floor(score)
        for (let i=0; i < integer; i++) {
          result.push(CLS_ON)
        }
        if (hasDecimal) {
          result.push(CLS_HALF)
        }
        while (result.length<LENGTH) {
          result.push(CLS_OFF)
        }
        return result
      }
    }
  }

</script>

<style lang="scss" rel="stylesheet/scss">
  .star{
    font-size:0;
    .star-item{
      display: inline-block;
      background-repeat: no-repeat;
    }
    &.star-48 {
        .star{
        width: 20px;
        height: 20px;
        margin-right: 22px;
        background-size: 20px 20px;
        &:last-child{
          margin-right: 0;
         }
        &.on {
          background-image: url("./star48_on@3x.png");
         }
        &.half {
           background-image: url("./star48_half@3x.png");
         }
        &.off {
           background-image: url("./star48_off@3x.png");
         }
      }
     }
  }
</style>
