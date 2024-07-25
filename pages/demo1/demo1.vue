<template>
	<view>
		<swiper indicator-dots indicator-color="blue" indicator-active-color="red" circular autoplay interval="2000" vertical>
			<swiper-item>111</swiper-item>
			<swiper-item>222</swiper-item>
			<swiper-item>333</swiper-item>
			<swiper-item>444</swiper-item>
		</swiper>
	</view>
	<view><image src="../../static/logo.png" class="pic1" mode="aspectFill" style="width: 50rpx; height: 50rpx"></image></view>
	<view>------</view>
	<navigator url="/pages/index/index" open-type="reLaunch">跳转</navigator>
	<view>------</view>
	<button @click="onClick">测试showModel</button>
</template>

<script setup>
function onClick() {
	uni.showModal({
		title: '是否删除？',
		cancelText: '取消',
		confirmText: '确定',
		success: (res) => {
			if (res.confirm)
				uni.showToast({
					title: '删除成功'
				});
		}
	});
}
</script>

<style lang="scss">
swiper {
	// vw 视图宽度,100代表宽度占满
	width: 100vw;
	height: 200px;
	border: 1px solid green;
	swiper-item {
		width: 100%;
		height: 100%;
		background: pink;
	}
	// 伪类选择器,四个item中,1 3是pink, 2 4是orange
	swiper-item:nth-child(2n) {
		background: orange;
	}
}
.pic1 {
	width: 200px;
	height: 200px;
}
</style>
