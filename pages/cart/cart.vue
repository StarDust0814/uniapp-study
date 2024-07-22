<template>
	<view class="out">
		<input type="text" :value="iptValue" @focus="onFocus" @blur="onBlur" :class="isActive ? 'active' : ''" />
		<image src="../../static/chicken.gif" class="pic" mode=""></image>
		<view class="item" v-for="item in goods" :key="item.id">
			<checkbox></checkbox>
			<text class="title">{{ item.name }}</text>
			<text class="del" @click="remove">删除</text>
		</view>
	</view>
</template>

<script setup>
import { ref } from 'vue';
const goods = ref([
	{ id: 1, name: '小米' },
	{ id: 2, name: '华为' },
	{ id: 3, name: '苹果' },
	{ id: 4, name: 'oppo' }
]);
// 控制active属性
const isActive = ref(false);
function remove(index) {
	goods.value.splice(index, 1);
}
const iptValue = ref('');
function onFocus(e) {
	console.log('触发聚焦');
	isActive.value = true;
}
function onBlur(e) {
	console.log('触发非聚焦');
	isActive.value = false;
}
</script>

<style lang="scss" scoped>
.out {
	padding: 0 20px;
	position: relative;
	margin-top: 40px;
	.item {
		padding: 10px 0;
		.del {
			color: red;
			margin-left: 30px;
		}
	}
	input {
		height: 40px;
		border: 1px solid red;
		position: relative;
		z-index: 2;
		background: #fff;
	}
	.pic {
		width: 24px;
		height: 24px;
		z-index: 1;
		position: absolute;
		// calc可以计算，居中位置
		left: calc(50% - 12px);
		top: 0px;
		transition: top 0.3s;
	}
	.pic.active {
		top: -24px;
	}
}
</style>
