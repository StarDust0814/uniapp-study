<template>
	<view class="box" hover-class="boxHover">
	<view class="inner" hover-class="innerHover" hover-stop-propagation>内部元素</view>
	</view>
	<view>-----</view>
	<text selectable user-select>支持选中的text标签包裹文本</text>
	<view>-----</view>
	<scroll-view scroll-x class="scrollView">
		<view class="scrollBox">scroll子元素</view>
		<view class="scrollBox">scroll子元素</view>
		<view class="scrollBox">scroll子元素</view>
		<view class="scrollBox">scroll子元素</view>
		<view class="scrollBox">scroll子元素</view>
		<view class="scrollBox">scroll子元素</view>
		<view class="scrollBox">scroll子元素</view>
		<view class="scrollBox">scroll子元素</view>
		<view class="scrollBox">scroll子元素</view>
		<view class="scrollBox">scroll子元素</view>
		<view class="scrollBox">scroll子元素</view>
	</scroll-view>
	<view>-----</view>
	<scroll-view scroll-y class="scrollView">
		<view>scroll子元素</view>
		<view>scroll子元素</view>
		<view>scroll子元素</view>
		<view>scroll子元素</view>
		<view>scroll子元素</view>
		<view>scroll子元素</view>
		<view>scroll子元素</view>
		<view>scroll子元素</view>
		<view>scroll子元素</view>
	</scroll-view>
</template>

<script setup>
	
</script>

<style lang='scss'>
	.box{
		width:200px;
		height:200px;
		background: #ccc;
	}
	.boxHover{
		background: orange;
		width: 300px;
	}
	.inner{
		width: 150px;
		height: 150px;
		background:green;
	}
	.innerHover{
		background: greenyellow;
	}
	.scrollView{
		width: 80%;
		height: 220px;
		border: 1px solid red;
		// 不允许换行
		white-space: nowrap;
		.scrollBox{
			width: 100px;
			height: 100px;
			background: green;
			// 块横向排列
			display: inline-block;
		}
	}
</style>
