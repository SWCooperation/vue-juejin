<template>
  <div class="books" ref="books" v-loading="loading">
    <scroll
      ref="scroll"
      :data="list"
      :scrollbar="scrollbar"
      :pullDownRefresh="pullDownRefresh"
      :pullUpLoad="pullUpLoad"
      @pullingDown="onPullingDown"
      @pullingUp="onPullingUp">
      <ul class="list-wrapper">
        <li class="list" v-for="(item, index) in list" :key="index">
          <img class="img" :src="item.url" alt="">
          <div>
            <span>{{item.title}}</span>
          </div>
          <span>{{item.price}}</span>
        </li>
      </ul>
    </scroll>
  </div>
</template>

<script type="text/ecmascript-6">
  import {requestParameters} from 'common/js/api';
  // import BScroll from 'better-scroll';
  import Scroll from 'base/scroll/scroll';

  export default {
    components: {
      Scroll,
    },
    data() {
      return {
        loading: false,
        list: [],
        scrollbar: {
          fade: true,
          interactive: false // 1.8.0 新增
        },
        pullDownRefresh: {
          threshold: 90,
          stop: 40
        },
        pullUpLoad: {
          threshold: 50
        }
      };
    },
    created() {
      this.pageNum = 1;
      this.init();
    },
    methods: {
      // 获取数据列表
      _getList() {
        return new Promise(resolve => {
          this.$get(requestParameters.url_getListByLastTime, {
            ...requestParameters.arg_getListByLastTime,
            pageNum: this.pageNum,
          }).then(json => {
            resolve(json);
          });
        });
      },
      // 初始化
      init() {
        this.loading = true;
        this._getList().then(json => {
          this.list = json.d;
        }).finally(() => {
          this.loading = false;
        });
      },
      // 下拉刷新
      onPullingDown() {
        this.pageNum = 1;
        this._getList().then(json => {
          this.list = json.d;
        }).catch(() => {
          this.$refs.scroll.forceUpdate();
        });
      },
      // 上拉加载更多
      onPullingUp() {
        this.pageNum++;
        this._getList().then(json => {
          if (json.d.length) {
            this.list = this.list.concat(json.d);
          } else {
            // 如果没有新数据
            this.$refs.scroll.forceUpdate()
          }
        }).catch(() => {
          this.$refs.scroll.forceUpdate();
        });
      },

    },
  };
</script>

<style lang="stylus" type="text/stylus" scoped>
  .books
    position: relative
    height: 100%
    overflow: hidden
    .list-wrapper
      .list
        display: flex
        .img
          width: 100px
          height: 140px
</style>
