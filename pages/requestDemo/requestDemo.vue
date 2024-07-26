<template>
	<view class="container">
		<view class="layout">
			<view class="box" v-for="item in pets" :key="item._id">
				<view class="pic">
					<image :src="item.url" mode="widthFix"></image>
				</view>
				<view class="text">{{ item.content }}</view>
				<view class="author">—— {{ item.author }}</view>
			</view>
		</view>
	</view>
</template>

<script setup>
const pets = ref([]);
// URL附加的参数可以填在 data字段
function network() {
	uni.request({
		url: 'https://tea.qingnian8.com/tools/petShow',
		data: {
			size: 10
		}
	}).then((res) => {
		console.log(res);
		pets.value = res.data.data;
	});
}
network();
</script>

<style lang="scss" scoped>
.container {
	.layout {
		padding: 50rpx;
		.box {
			margin-bottom: 60rpx;
			box-shadow: 0 10rpx 30rpx rgba(0, 0, 0, 0.08);
			.pic {
				image {
					width: 100%;
				}
			}
			.text {
				padding: 5rpx;
				color: #333;
				font-size: 36rpx;
			}
			.author {
				padding: 0 30rpx 30rpx;
				text-align: right;
				color: #888;
				font-size: 24rpx;
			}
		}
	}
}
</style>
