<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar" alt="头像" />
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <h2>{{ seller.name }}</h2>
        </div>
        <div class="description">
          {{ seller.description }}/{{ seller.deliveryTime }}分钟送达
        </div>
        <div v-if="seller.supports" class="supports">
          <i :class="supportsIconClassList[seller.supports[0].type]"></i>
          <span>{{ seller.supports[0].description }}</span>
        </div>
        <div class="supports-count">
          <span v-if="seller.supports" class="count">{{ seller.supports.length }}个</span>
          <span class="icon-keyboard_arrow_right"></span>
        </div>
      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{ seller.bulletin }}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
  </div>
</template>

<script>
export default {
  props: ["seller"],
  data() {
    return {
      supportsIconClassList: []
    };
  },
  methods: {},
  created() {
    this.supportsIconClassList = ['decrease', 'discount', 'guarantee', 'invoice', 'special'];
  }
};
</script>

<style lang="scss" scoped>
@import "../../common/styles/index.scss";
@import '../../common/styles/style.css';

.header {
  background-color: rgba(7, 17, 27, 0.5);

  .content-wrapper {
    position: relative;
    display: flex;
    padding: 0.48rem 0.24rem 0.36rem 0.48rem;

    .avatar {
      width: 1.28rem;
      height: 1.28rem;

      img {
        width: 100%;
        height: 100%;
        border-radius: 4px;
      }
    }

    .content {
      padding-top: 0.04rem;
      margin-left: 0.32rem;
      color: #fff;

      .title {
        display: flex;
        align-items: center;

        .brand {
          display: inline-block;
          width: 0.6rem;
          height: 0.36rem;
          @include img-dpr("./images/brand");
          margin-right: 0.12rem;
        }

        h2 {
          font-size: 0.32rem;
          line-height: 0.36rem;
          font-weight: bold;
        }
      }

      .description {
        font-size: 0.24rem;
        line-height: 0.24rem;
        margin-top: 0.16rem;
      }

      .supports {
        display: flex;
        align-items: center;
        margin-top: 0.2rem;

        i {
          display: inline-block;
          width: 0.24rem;
          height: 0.24rem;
          margin-right: 0.08rem;

          &.decrease {
            @include img-dpr("./images/decrease_1");
          }
          &.discount {
            @include img-dpr("./images/discount_1");
          }
          &.guarantee {
            @include img-dpr("./images/guarantee_1");
          }
          &.invoice {
            @include img-dpr("./images/invoice_1");
          }
          &.special {
            @include img-dpr("./images/special_1");
          }
        }

        span {
          font-size: 0.2rem;
          line-height: 0.24rem;
        }
      }

      .supports-count {
        position: absolute;
        right: 0.24rem;
        bottom: 0.36rem;
        padding: 0.14rem 0.16rem;
        border-radius: 0.24rem;
        background-color: rgba(0, 0, 0, 0.2);
        font-size: 0.2rem;
        line-height: 0.2rem;
        color: #fff;
      }
    }
  }

  .bulletin-wrapper {
    width: 100%;
    height: 0.56rem;
    background-color: rgba(7, 17, 27, 0.2);
    padding: 0 0.24rem;
    font-size: 0.2rem;
    line-height: 0.56;
    text-overflow: ellipsis;
    white-space: nowrap;
    color: #fff;
    overflow: hidden;
    box-sizing: border-box;

    .bulletin-title {
      display: inline-block;
      width: 0.44rem;
      height: 0.24rem;
      @include img-dpr('./images/bulletin');
    }

    .bulletin-text {
      margin-left: 0.08rem;
      margin-right: 0.08rem;
    }
  }
}
</style>
