<template>
	<view class="box" hover-class="boxHover">
	<view class="inner" hover-class="innerHover" hover-stop-propagation>内部元素</view>
	</view>
	<view>-----</view>
	<text selectable user-select>支持选中的text标签包裹文本</text>
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
</style>
