<template>
  <div id="app">
    <div class="list">
      <div class="list-content">
        <h1 class="title">汇聚上万条优秀创意案例，轻松匹配所需内容，打开您的脑洞</h1>
        <div class="modality">
          <h1 class="modality-title">形式:</h1>
          <ul class="content-wrapper">
            <li v-for="(content, index) in modalityMap"
                class="modality-content"
                @click="changeModality(index)"
                :class="{'active':modalityType === modalityMap[index]}"
            >{{modalityMap[index]}}</li>
          </ul>
        </div>
        <div class="time">
          <span class="time-title">时间节点:</span>
          <ul class="content-wrapper">
            <li v-for="(time, index) in timeMap"
                class="time-content"
                @click="changeTime(index)"
                :class="{'active': timeType === timeMap[index]}">
              {{timeMap[index]}}
            </li>
          </ul>
        </div>
      </div>
    </div>
    <contents :contents="contents"
              :modalityType="modalityType"
              :timeType="timeType"></contents>
  </div>
</template>

<script>
  import contents from './components/contents/contents.vue';

//  const url = 'http://www.wucai.com/service_new/?m=Home&c=Search&a=chuangyi&page=1&count=21&days=%E6%83%85%E4%BA%BA%E8%8A';

  const All = '不限';
  export default {
    data () {
      return {
        contents: {},
        modalityType: All,
        timeType: All
      };
    },
    created: function() {
      this.modalityMap = [ '不限', 'H5', '海报', '视频' ];
      this.timeMap = [ '不限', '元旦', '春节', '感恩节', '母亲节', '父亲节', '双十一',
        '情人节', '618', '国庆节'];
      this.$http.get('api/info').then((response) => {
        response = response.body;
        console.log(response);
        this.contents = response.data;
        console.log(this.contents);
    });
    },
    methods: {
      changeModality (index) {
        this.modalityType = this.modalityMap[index];
      },
      changeTime (index) {
        this.timeType = this.timeMap[index];
      }
    },
    components: {
      contents
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylue">
  @import "./common/normalize.css";
  #app
   padding: 20px 10% 0 3%
  .list
      .list-content
        .title
          font-size: 1.17em
          font-weight: bold
        .modality
          .modality-title
            display: inline-block
            font-size: 22px
            font-weight: bold
            color: #666
            line-height: 2
            margin-right: 70px
          .content-wrapper
            display: inline-block
            .modality-content
              display: inline-block
              height: 44px
              line-height: 2
              padding-right: 10px
              cursor: pointer
              color: #005aa0
              margin-right: 20px
              font-size: 22px
              &:hover
                color: red
              &.active
                color: #34c26f
        .time
          .time-title
            display: inline-block
            font-size: 22px
            font-weight: bold
            color: #666
            line-height: 2
            margin-right: 25px
          .content-wrapper
            display: inline-block
            .time-content
              display: inline-block
              height: 44px
              line-height: 2
              padding-right: 10px
              cursor: pointer
              color: #005aa0
              margin-right: 20px
              font-size: 22px
              &:hover
                color: red
              &.active
                color: #34c26f
</style>
