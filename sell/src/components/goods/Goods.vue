<template>
  <div class="goods">
    <div class="menu-wrapper">
			<ul>
				<li v-for="(item, index) in goods" :key="index" class="menu-item">
					<div>
						<i v-show="item.type > 0" :class="supportsIconClassList[item.type]"></i>
						<span>{{ item.name }}</span>
					</div>
				</li>
			</ul>
		</div>
    <div class="foods-wrapper">
			<ul>
				<li class="food-list" v-for="(item, index) in goods" :key="index">
					<h4 class="list-name">{{ item.name }}</h4>
					<ul class="food-items">
						<li class="food-item" v-for="(food, index) in item.foods" :key="index">
							<div class="food-icon">
								<img :src="food.icon" alt="食品图标">
							</div>
							<div class="content">
								<h3 class="food-name">{{ food.name }}</h3>
								<p class="food-description">{{ food.description }}</p>
								<div class="extra">
									<span>月售{{ food.sellCount }}份</span>
									<span>好评率{{ food.rating }}%</span>
								</div>
								<div class="price">
									<span class="curPrice">￥{{ food.price }}</span>
									<del class="oldPrice" v-if="food.oldPrice">￥{{ food.oldPrice }}</del>
								</div>
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
  </div>
</template>

<script>
import Axios from 'axios';

/* 定义常量-错误码 */
const ERR_NO = 0;

export default {
  props: ["seller"],
  data() {
    return {
			goods: []
		}
	},
	methods: {
		/**
		 * 异步获取并设置 goods 数据
		 * @param {String} 请求地址
		 */
		async getGoods(url) {
			try {
				let {data} = await Axios.get(url);
				if (data.errno === ERR_NO) {
					this.goods = data.data;
				}
			} catch (error) {
				console.log('获取数据失败!' + error);
			}
		}
	},
	created() {
		// 小技巧：为 icon 动态添加类名，根据不同类名显示不同图标
		this.supportsIconClassList = ['decrease', 'discount', 'guarantee', 'invoice', 'special'];
		// 调用异步函数
		this.getGoods('/api/goods');
	},
};
</script>

<style lang="scss" scoped>
@import '../../common/styles/index.scss';

.goods {
  position: absolute;
  top: 3.49rem;
  bottom: 0.72rem;
  left: 0;
  display: flex;
  width: 100%;
	overflow: hidden;

  .menu-wrapper {
    width: 1.6rem;
    background-color: #f3f5f7;
		padding: 0 0.24rem;
		box-sizing: border-box;

		.menu-item {
			display: flex;
			align-items: center;
			width: 100%;
			height: 1.08rem;
			border-bottom: 1px solid #dbdee1;
			box-sizing: border-box;

			i {
				display: inline-block;
				margin-top: 0.02rem;
				width: 0.24rem;
				height: 0.24rem;
				vertical-align: top;

				&.decrease {
					@include img-dpr("./images/decrease_3");
				}
				&.discount {
					@include img-dpr("./images/discount_3");
				}
				&.guarantee {
					@include img-dpr("./images/guarantee_3");
				}
				&.invoice {
					@include img-dpr("./images/invoice_3");
				}
				&.special {
					@include img-dpr("./images/special_3");
				}
			}

			span {
				font-size: 0.24rem;
				line-height: 0.28rem;
				color: rgb(7, 17, 27);
				vertical-align: top;
			}
		}
  }

  .foods-wrapper {
    flex: 1;

		.list-name {
			display: flex;
			align-items: center;
			width: 100%;
			height: 0.52rem;
			background-color: #f3f5f7;
			border-left: 4px solid #d9dde1;
			padding-left: 0.28rem;
			box-sizing: border-box;
			font-size: 0.24rem;
			line-height: 0.52rem;
			color: rgb(147, 153, 159);
		}

		.food-items {
			padding: 0 0.36rem;
		}

		.food-item {
			display: flex;
			width: 100%;
			padding: 0.36rem 0;
			border-bottom: 1px solid #d9dde1;
			box-sizing: border-box;

			&:nth-last-child(1) {
				border-bottom: 0;
			}

			.food-icon {
				width: 1.14rem;
				height: 1.14rem;
				margin-right: 0.2rem;

				img {
					width: 100%;
					height: 100%;
				}
			}

			.content {
				padding-top: 0.04rem;

				.food-name {
					font-size: 0.28rem;
					line-height: 0.28rem;
					color: rgb(7, 17, 27);
				}

				.food-description,
				.extra {
					font-size: 0.2rem;
					line-height: 0.2rem;
					color: rgb(147, 153, 159);
					margin-top: 0.16rem;
				}

				.extra {
					span {
						&:nth-child(1) {
							margin-right: 0.24rem;
						}
					}
				}

				.price {
					line-height: 0.48rem;
					font-weight: 700;

					.curPrice {
						font-size: 0.24rem;
						color: rgb(240, 20, 20);
					}

					.oldPrice {
						font-size: 0.2rem;
						color: rgb(147, 153, 159);
					}
				}
			}
		}
  }
}
</style>