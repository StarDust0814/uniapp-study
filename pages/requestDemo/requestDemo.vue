<template>
	<view class="container">
		<view class="menu">
			<uni-segmented-control :current="1" :values="[11, 22, 33]" @clickItem="onClickItem" styleType="button" activeColor="#2B9939"></uni-segmented-control>
			<view class="layout">
				<view class="box" v-for="(item, index) in pets" :key="item._id">
					<view class="pic">
						<image lazy-load :src="item.url" mode="widthFix" @click="onPreview(index)"></image>
					</view>
					<view class="text">{{ item.content }}</view>
					<view class="author">—— {{ item.author }}</view>
				</view>
			</view>
			<view class="float">
				<view class="item" @click="onRefresh"><uni-icons type="refreshempty"></uni-icons></view>
				<view class="item" @click="onTop"><uni-icons type="arrow-up"></uni-icons></view>
			</view>
			<view class="loadMore">
				<uni-load-more status="loading"></uni-load-more>
			</view>
		</view>
	</view>
</template>

<script setup>
const pets = ref([]);
// URL附加的参数可以填在 data字段
function network() {
	uni.showLoading();
	uni.request({
		url: 'https://tea.qingnian8.com/tools/petShow',
		data: {
			size: 10
		},
		header: {
			'access-key': '500632'
		}
	})
		.then((res) => {
			uni.hideLoading();
			if (res.data.errCode === 0) {
				// 处理成新的数组添加在原数组之后
				pets.value = [...pets.value, ...res.data.data];
			} else if (res.data.errCode === 400) {
				uni.showToast({
					title: res.data.errMsg,
					icon: 'none'
				});
			}
		})
		.catch((err) => {
			uni.hideLoading();
			uni.showToast({
				title: '网络错误',
				icon: 'none'
			});
		})
		.finally(() => {
			uni.hideLoading();
			uni.stopPullDownRefresh();
		});
}
network();

onReachBottom(() => {
	network();
});

onPullDownRefresh(() => {
	// 重新渲染，清空原本的数据
	pets.value = [];
	network();
});

// 预览图片
function onPreview(index) {
	// 将数组中每个元素的某个属性单独抽离出来组成一个新数组
	let urls = pets.value.map((item) => item.url);
	uni.previewImage({
		urls,
		current: index
	});
}

function onRefresh() {
	uni.startPullDownRefresh();
}
function onTop() {
	uni.pageScrollTo({
		duration: 100,
		scrollTop: 0
	});
}
</script>

<style lang="scss" scoped>
.container {
	.menu {
		padding: 50rpx 50rpx 0;
	}
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
	.float {
		position: fixed;
		right: 30rpx;
		bottom: 80rpx;
		// 设置移动设备中的底部安全区域（如虚拟HOME键等，避免自定义组件与其重叠）
		padding-bottom: env(safe-area-inset-bottom);
		.item {
			width: 90rpx;
			height: 90rpx;
			background: rgba(255, 255, 255, 0.9);
			border-radius: 50%;
			border: 1px solid #eee;
			display: flex;
			justify-content: center;
			align-items: center;
			margin-bottom: 20rpx;
		}
	}
	.loadMore {
		padding-bottom: calc(env(safe-area-inset-bottom) + 52rpx);
	}
}
</style>
