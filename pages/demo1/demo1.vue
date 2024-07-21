<template>
	<view>
		<swiper indicator-dots indicator-color="blue" indicator-active-color="red" circular autoplay interval="2000" vertical>
			<swiper-item>111</swiper-item>
			<swiper-item>222</swiper-item>
			<swiper-item>333</swiper-item>
			<swiper-item>444</swiper-item>
		</swiper>
	</view>
	<view><image src="../../static/logo.png" class='pic1' mode='aspectFill'></image></view>
	<view>------</view>
	<navigator url='/pages/index/index' open-type="reLaunch">跳转</navigator>
</template>

<script setup>
	
</script>

<style lang='scss'>
swiper{
	// vw 视图宽度,100代表宽度占满
	width: 100vw;
	height: 200px;
	border: 1px solid green;
	swiper-item{
		width: 100%;
		height: 100%;
		background:pink;
	}
	// 伪类选择器,四个item中,1 3是pink, 2 4是orange
	swiper-item:nth-child(2n){
		background: orange;
	}
}
.pic1{
	width: 200px;
	height: 200px;
}
</style>
