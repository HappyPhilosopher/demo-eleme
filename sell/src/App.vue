<template>
  <div id="app">
    <Header :seller="seller" />

    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import Header from './components/header/Header';
import Axios from 'axios';

export default {
  name: 'App',
  components: {
    Header
  },
  data() {
    return {
      seller: {}
    }
  },
  methods: {
    /**
     * 异步获取并设置 seller 数据
     * @param {String} 请求地址
     */
    async getSeller(url) {
        let response = await Axios.get(url);
        let data = await response.data;
        if (data.errno === 0) {
            this.seller = data.data
        }
    }
  },
  created() {
    this.getSeller('/api/seller');
  },
}
</script>

<style lang="scss" scoped>
@import './common/styles/index.scss';

.tab {
  display: flex;
  align-items: center;
  width: 100%;
  height: 0.8rem;
  border-bottom: 1px solid rgba(7, 17, 27, 0.1);

  .tab-item {
    flex: 1;

    a {
      display: flex;
      justify-content: center;
      width: 100%;
      height: 100%;
      // @include fontsize(28px);
      font-size: 0.28rem;
    }

    .router-link-active {
      color: rgb(240, 20, 20);
    }
  }
}
</style>