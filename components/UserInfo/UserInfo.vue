<template>
	<image src="../../static/logo.png"></image>
	<view>用户名：{{ username }}</view>
	<!--通过emit事件，自定义子组件的按钮，在点击时触发向外传递的函数和对应的参数-->
	<button @click="onClick">emit事件</button>
	<button @click="onChange">另一种emit事件</button>
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
const emit = defineEmits(['add', 'change']);
function onClick() {
	emit('add', Math.random());
}
function onChange() {
	emit('change', Math.random());
}
</script>

<style lang="scss"></style>
