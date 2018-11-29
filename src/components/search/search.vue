<template>
  <div class="search">
    <div class="top-img">
      <!-- <img src="" alt=""> -->
    </div>
    <div class="tab">

      <div class="tab-li" v-for="(item,index) in tabList" :key="index">
        <span>{{item.name}}</span>
      </div>

    </div>
    <ul>
      <li class="list" v-for="(item,index) in list" :key="index">
        <img src="" alt="">
      </li>
    </ul>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    data() {
      return {
        tabList: [
          {name: '本周最热', url: '', img: ''},
          {name: '收藏夹', url: '', img: ''},
          {name: '活动', url: '', img: ''}
        ],
        list: []
      };
    },
  };
</script>

<style lang="stylus" type="text/stylus" scoped>
  .search
    background: #d8d8d8
    height: 100%
    overflow: hidden
    .tab
      width 100%
      height 80px
      line-height 80px
      background #fff
      display flex
      .tab-li
        flex 1
        display inline-block
        text-align center
</style>
