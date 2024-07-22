<template>
	<image src="../../static/logo.png"></image>
	<view>用户名：{{ username }}</view>
</template>

<script setup>
// 父子组件通过 props传值，在组件中定义可以传递的参数名称
defineProps(
	{
		username: {
			type: String,
			default: '匿名'
		}
	},
	{
		avatar: {
			type: String,
			default: '../../static/logo.png'
		}
	}
);
</script>

<style lang="scss"></style>
