<template>
	<view class="container">
		<view class="layout">
			<view class="box" v-for="(item, index) in pets" :key="item._id">
				<view class="pic">
					<image lazy-load :src="item.url" mode="widthFix" @click="onPreview(index)"></image>
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
		},
		header: {
			'access-key': '500632'
		}
	}).then((res) => {
		console.log(res);
		pets.value = res.data.data;
	});
}
network();

// 预览图片
function onPreview(index) {
	// 将数组中每个元素的某个属性单独抽离出来组成一个新数组
	let urls = pets.value.map((item) => item.url);
	uni.previewImage({
		urls,
		current: index
	});
}
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
