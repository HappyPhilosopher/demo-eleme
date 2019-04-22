<template>
  <div class="header">
    <div class="content-wrapper">
      <!-- 商家头像 -->
      <div class="avatar">
        <img :src="seller.avatar" alt="头像" />
      </div>
      <!-- 商家内容 -->
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
        <div class="supports-count" @click="showDetails()">
          <span v-if="seller.supports" class="count">{{ seller.supports.length }}个</span>
          <span class="icon-keyboard_arrow_right"></span>
        </div>
      </div>
    </div>
    <!-- 商家公告 -->
    <div class="bulletin-wrapper" @click="showDetails()">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{ seller.bulletin }}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <!-- 背景 -->
    <div class="header-background">
      <img :src="seller.avatar" alt="背景图" width="100%" height="100%">
    </div>
    <!-- 商家详情 -->
    <transition name="showDetail">
      <div class="detail" v-show="detailShow">
        <div class="detail-wrapper">
          <div class="detail-main">
            <h2>{{ seller.name }}</h2>
            <div class="star-wrapper">
              <Star :size="48" :score="seller.score"/>
            </div>
            <h3>
              <i></i>
              <span>优惠信息</span>
              <i></i>
            </h3>
            <ul class="supports" v-if="seller.supports">
              <li v-for="(item, index) in seller.supports" :key="index" class="support-item">
                <i :class="supportsIconClassList[index]"></i>
                <span>{{ item.description }}</span>
              </li>
            </ul>
            <h3>
              <i></i>
              <span>商家公告</span>
              <i></i>
            </h3>
            <div class="bulletin">
              <p>{{ seller.bulletin }}</p>
            </div>
          </div>
        </div>
        <div class="detail-close" @click="hideDetails()">
          <i class="icon-close"></i>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import Star from '../star/Star';

export default {
  props: ['seller'],
  data() {
    return {
      // supportsIconClassList: [],
      detailShow: false
    };
  },
  methods: {
    showDetails() {
      this.detailShow = true;
    },
    hideDetails() {
      this.detailShow = false;
    }
  },
  created() {
    // 小技巧：为 icon 动态添加类名，根据不同类名显示不同图标
    this.supportsIconClassList = ['decrease', 'discount', 'guarantee', 'invoice', 'special'];
  },
  components: {
    Star
  }
};
</script>

<style lang="scss" scoped>
@import "../../common/styles/index.scss";
@import '../../common/styles/style.css';

.header {
  position: relative;
  background-color: rgba(7, 17, 27, 0.5);
  overflow: hidden;

  .content-wrapper {
    position: relative;
    display: flex;
    padding: 0.48rem 0.24rem 0.36rem 0.48rem;

    /* 商家头像 */
    .avatar {
      width: 1.28rem;
      height: 1.28rem;

      img {
        width: 100%;
        height: 100%;
        border-radius: 4px;
      }
    }

    /* 商家内容 */
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

  /* 商家公告 */
  .bulletin-wrapper {
    position: relative;
    width: 100%;
    height: 0.56rem;
    background-color: rgba(7, 17, 27, 0.2);
    padding: 0 0.44rem 0 0.24rem;
    font-size: 0.2rem;
    line-height: 0.56rem;
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
      vertical-align: top;
      margin-top: 0.16rem;
    }

    .bulletin-text {
      margin-left: 0.08rem;
      margin-right: 0.08rem;
    }

    .icon-keyboard_arrow_right {
      position: absolute;
      top: 50%;
      right: 0.24rem;
      transform: translateY(-50%);
      font-size: 0.2rem;
    }
  }

  /* header 背景图 */
  .header-background {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    filter: blur(10px);
    z-index: -1;
  }

  /* 显示、隐藏详细内容过渡动画 */
  .showDetail-enter,
  .showDetail-leave-to {
    opacity: 0;
  }
  .showDetail-enter-active,
  .showDetail-leave-active {
    transition: all 0.5s ease;
  }

  /* 商家详情 */
  .detail {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    min-height: 100%;
    display: flex;
    flex-direction: column;
    background-color: rgba(0, 0, 0, 0.8);
    backdrop-filter: blur(10px);  // 该属性为实验性属性，大多数浏览器不支持
    z-index: 100;

    .detail-wrapper {
      flex: 1;
      width: 100%;
      color: #fff;
      box-sizing: border-box;

      .detail-main {
        margin-top: 1.28rem;
        padding: 0 0.72rem;

        h2 {
          font-size: 0.32rem;
          line-height: 0.32rem;
          text-align: center;
          font-weight: 700;
        }

        .star-wrapper {
          display: flex;
          align-items: center;
          justify-content: center;
          height: 0.48rem;
          margin-top: 0.32rem;
        }

        h3 {
          display: flex;
          align-items: center;
          margin-top: 0.56rem;

          i {
            flex: 1;
            display: block;
            height: 1px;
            background-color: rgba(255, 255, 255, 0.2);
          }

          span {
            padding: 0 0.24rem;
            font-size: 0.28rem;
            font-weight: 700;
            color: #fff;
          }
        }

        .supports {
          margin-top: 0.48rem;
          padding: 0 0.24rem;

          .support-item {
            display: flex;
            align-items: center;
            margin-top: 0.24rem;

            &:nth-child(1) {
              margin-top: 0;
            }

            i {
              display: block;
              width: 0.32rem;
              height: 0.32rem;
              margin-right: 0.12rem;
              
              &.decrease {
                @include img-dpr('./images/decrease_2');
              }
              &.discount {
                @include img-dpr('./images/discount_2');
              }
              &.guarantee {
                @include img-dpr('./images/guarantee_2');
              }
              &.invoice {
                @include img-dpr('./images/invoice_2');
              }
              &.special {
                @include img-dpr('./images/special_2');
              }
            }

            span {
              font-size: 0.24rem;
            }
          }
        }

        .bulletin {
          margin-top: 0.48rem;
          padding: 0 0.24rem;
          font-size: 0.24rem;
          line-height: 0.48rem;
        }
      }
    }

    .detail-close {
      width: 100%;
      height: 1.28rem;
      font-size: 0.64rem;
      color: rgba(255, 255, 255, 0.5);
      text-align: center;
    }
  }
}
</style>
