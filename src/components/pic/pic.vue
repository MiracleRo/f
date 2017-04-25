<template>
    <transition name="move">
      <div class="pic" v-show="showFlag">
        <div class="top">
          <div class="button" @click="hide"></div>
        </div>
        <div class="pic-wrapper">
          <div class="pic-left">
            <p class="title">#{{pic.title}}#视频</p>
            <div class="abs"><span class="desc">创意描述:</span>{{pic.abstract}}</div>
          </div>
          <div class="pic-right">
            <img :src="pic.pic">
            <div class="url">来源{{pic.url}}</div>
          </div>
        </div>
      </div>
    </transition>
</template>

<script>
  export default{
    props: {
      pic: {
        type: Object
      }
    },
    data () {
      return {
        showFlag: false
      };
    },
    methods: {
      show() {
        this.showFlag = true;
      },
      hide() {
        this.showFlag = false;
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylue">
  .pic
    padding: 20px 50px
    height: 100%
    position: fixed
    left: 0
    top: 0
    bottom: 0
    z-index: 30
    width: 100%
    background: #fff
    transform: translate3d(0, 0, 0)
    &.move-enter-active, &.move-leave-active
      transition: all 0.2s linear
    &.move-enter, &.move-leave-active
      transform: translate3d(100%, 0, 0)
    .top
      height: 65px
      box-shadow: 1px 1px 3px rgba(80, 80, 80, 0.1)
      padding: 10px 0
      .button
        background: url(./cbp-sprite.png) no-repeat scroll -92px -92px transparent;
        height: 44px;
        width: 44px;
        margin: auto;
    .pic-wrapper
      margin-top: 20px
      .pic-left
        display: inline-block
        padding: 0px 30px 0 0
        line-height: 2
        width: 40%
        vertical-align:top
        .title
          margin-bottom: 15px
          font-size: 27px
          font-weight: bold
          line-height: 2
        .abs
           font-size: 18px
           line-height: 2
           .desc
              font-weight: bold
      .pic-right
        display: inline-block
        width: 500px
        position: relative
        height: 340px
        img
          height: 100%
          width: 100%
          max-height: 500px;
          max-width: 500px;
          margin-bottom: 10px;
        .url
          font-size: 12px;
          word-wrap: break-word;
</style>
