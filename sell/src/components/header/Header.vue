<template>
  <div class="header">
		<div class="content-wrapper">
			<div class="avatar">
				<img :src="seller.avatar" alt="头像">
			</div>
			<div class="content">
				<div class="title">
					<span class="brand"></span>
					<h2>{{ seller.name }}</h2>
				</div>
				<div class="description">
					{{ seller.description }}/{{ seller.deliveryTime }}分钟送达
				</div>
				<div v-if="seller.supports" :class="supports">
					<i></i>
					<span>{{ seller.supports[0].description }}</span>
				</div>
			</div>
		</div>
		<div class="bulletin-wrapper"></div>
	</div>
</template>

<script>
export default {
	props: ['seller'],
  data() {
		return {
      supports: []
    };
  },
  methods: {},
  created() {
    
  }
};
</script>

<style lang="scss" scoped>
@import '../../common/styles/index.scss';

.header {
	background-color: rgba(7, 17, 27, 0.5);

	.content-wrapper {
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
					@include img-dpr('./images/brand');
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

			.support {
				display: flex;
				align-items: center;
				margin-top: 0.2rem;

				i {
					display: inline-block;
					width: 0.24rem;
					height: 0.24rem;
					@include img-dpr('./images/decrease_1');
					margin-right: 0.08rem;
				}

				span {
					font-size: 0.2rem;
					line-height: 0.24rem;
				}
			}
		}
	}
}
</style>
