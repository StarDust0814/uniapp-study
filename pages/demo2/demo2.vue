<template>
	<view>
		<button size="mini" type="primary">按钮</button>
	</view>
	<view>-----</view>
	<input type="number" placeholder="请输入内容" />
	<view>-----</view>
	{{ a + b }}
	<view>-----</view>
	{{ num2 }}
	{{ obj }}
</template>

<script setup>
const a = 5,
	b = 3;
import { ref } from 'vue';
// 将一个字面量包装成一个对象
let num2 = ref(10);
console.log(num2.value);
// 注意这里修改ref变量要读取到 .value属性
setInterval(() => {
	num2.value++;
}, 1000);
// ref同样支持数组、对象等复杂类型
let obj = ref({ name: 'frank', age: 25 });
console.log(obj.value.name);
</script>

<style lang="scss"></style>

<style lang="scss"></style>
