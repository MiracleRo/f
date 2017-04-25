<template>
  <div class="contents-wrapper">
      <ul class="contents">
        <li v-for="item in contents" class="content"
            v-show="needShow(item.days, item.modality)">
          <div class="img-wrapper">
            <img :src="item.pic" @click="selectPic(item)">
          </div>
          <span class="brand" @click="selectPic(item)">{{item.brand}}</span>
          <a class="title" :href="item.url">{{item.title}}</a>
        </li>
      </ul>
      <pic ref="pic" :pic="selectedPic"></pic>
  </div>
</template>

<script type="text/ecmascript-6">
  import pic from '../pic/pic.vue';
  const All = '不限';
  export default{
    data() {
      return {
        selectedPic: {}
      };
    },
    props: {
      contents: {
        type: Array
      },
      modalityType: {
        type: String,
        default: All
      },
      timeType: {
        type: String,
        default: All
      }
    },
    methods: {
      selectPic: function(pic) {
        this.selectedPic = pic;
        console.log(this.selectedPic);
        this.$refs.pic.show();
      },
      needShow(days, modality) {
        if (this.timeType === All && this.modalityType === All) {
          return true;
        } else {
          console.log(this.timeType + '' + days + '' +
            this.modalityType + '' + modality);
          return (this.timeType === days || this.modalityType === modality);
        }
      }
    },
    components: {
      pic
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylue">
    .contents-wrapper
      margin-top: 20px
      width: 100%
      .contents
        font-size: 0
        width: 100%
        .content
          display: inline-block
          width: 32%
          margin-right: 10px
          vertical-align:top
          margin-bottom: 30px
          &:last-child
            margin-right: 0
          .img-wrapper
            height: 180px
            margin-bottom: 20px
            img
              width: 100%
              height: 100%
          .brand
            font-size: 10px
            display: block
            cursor: pointer
          .title
            display: inline-block
            cursor: pointer
            font-size: 24px
            color: #333333
            line-height: 28px
            margin-top: 10px
            font-weight: bold
            &:hover
              color: #3BBF69
</style>
