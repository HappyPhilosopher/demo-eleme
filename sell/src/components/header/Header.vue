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
				<div v-if="seller.support" class="support">
					<i></i>
					<span>{{ seller.support[0].description }}</span>
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
    return {};
  },
  methods: {},
  created() {}
};
</script>

<style lang="scss" scoped>
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
				border-radius: 0.04rem;
			}
		}

		.content {
			padding-top: 0.04rem;
			margin-left: 0.32rem;


		}
	}
}
</style>