<template>
  <div class="star" :class="starType">
		<span class="star-item" v-for="(itemClass, index) in itemClasses" :key="index" :class="itemClass"></span>
	</div>
</template>

<script>
export default {
	props: {
		size: Number,
		score: Number
	},
	computed: {
		/**
		 * 动态添加类名，由父组件传值（size）定义，如 .star-48, .star-36, .star-24
		 */
		starType() {
			return `star-${this.size}`;
		},
		/**
		 * 动态添加类名组，根据父组件传值（score）定义
		 * 根据需求，评级由“全星”、“半星”、“无星”组成，所以类名组中应由具体“星星”个数决定
		 * @return {Array} 返回类名数组
		 */
		itemClasses() {
			// 定义常量-星星总个数
			const LENGTH = 5;
			// 定义常量-“全星”、“半星”、“无星”类名
			const CLS_ON = 'on';
			const CLS_HALF = 'half';
			const CLS_OFF = 'off';
			// 定义类名数组，接收星星状态
			let result = [];
			// 格式化评分，0.5 为分界点
			let scoreFormat = Math.floor(this.score * 2) / 2;
			// 判断格式化后的评分是否为小数
			let hasDecimal = scoreFormat % 1 !== 0;
			// 提取评分整数
			let scoreInteger = Math.floor(scoreFormat);
			// 遍历有多少个“全星”，添加到 result
			for (let i = 0; i < scoreInteger; i++) {
				result.push(CLS_ON);
			}
			// 如果格式化后的评分为小数，则添加“半星”
			if (hasDecimal) {
				result.push(CLS_HALF);
			}
			// 根据星星总个数，将剩余位置添加“无星”
			while (result.length < LENGTH) {
				result.push(CLS_OFF);
			}
			return result;
		}
	},
};
</script>

<style lang="scss" scoped>
@import '../../common/styles/index.scss';

.star {
	display: flex;
	justify-content: center;

	.star-item {
		display: inline-block;
	}

	&.star-48 {
		.star-item {
			width: 0.4rem;
			height: 0.4rem;
			margin-right: 0.44rem;
			&:last-child(1) {
				margin-right: 0;
			}
	
			&.on {
				@include img-dpr('./images/star48_on');
			}
			&.half {
				@include img-dpr('./images/star48_half');
			}
			&.off {
				@include img-dpr('./images/star48_off');
			}
		}
	}

	&.star-36 {
		.star-item {
			width: 0.3rem;
			height: 0.3rem;
			margin-right: 0.12rem;
			&:last-child(1) {
				margin-right: 0;
			}
	
			&.on {
				@include img-dpr('./images/star36_on');
			}
			&.half {
				@include img-dpr('./images/star36_half');
			}
			&.off {
				@include img-dpr('./images/star36_off');
			}
		}
	}

	&.star-24 {
		.star-item {
			width: 0.2rem;
			height: 0.2rem;
			margin-right: 0.6rem;
			&:last-child(1) {
				margin-right: 0;
			}
	
			&.on {
				@include img-dpr('./images/star24_on');
			}
			&.half {
				@include img-dpr('./images/star24_half');
			}
			&.off {
				@include img-dpr('./images/star24_off');
			}
		}
	}
}
</style>
