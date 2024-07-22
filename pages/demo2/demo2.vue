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
	<view>-----</view>
	<!--:src 为 v-bind:src 省略写法-->
	<image :src="picurl"></image>
	<button type="primary" :loading="false">按钮加载</button>
	<view>-----</view>
	<view class="box" :class="{ active: isActive }"></view>
	<!--内联样式 v-bind :style-->
	<view :style="{ width: '300px', height: 200 + 'px', background: 'blue' }"></view>
	<view>-----</view>
	<!--事件绑定 v-on-->
	<view class="boxClick" @click="onClick"></view>
	<!--v-for渲染-->
	<view class="box" v-for="(item, index) in 10">box模块-{{ index }}</view>
	<view v-for="(item, index) in list" :key="item.id">{{ item.id }}--{{ item.name }}--{{ item.age }}</view>
	<view>-----</view>
	<input type="text" placeholder="请输入名" v-model="firstName" />
	<input type="text" placeholder="请输入姓" v-model="lastName" />
	{{ fullName }}
</template>

<script setup>
// vue使用
const a = 5,
	b = 3;
import { ref, computed, watch } from 'vue';
// 将一个字面量包装成一个对象
let num2 = ref(10);
console.log(num2.value);
const isActive = ref(false);
// 注意这里修改ref变量要读取到 .value属性
setInterval(() => {
	num2.value++;
}, 1000);
// ref同样支持数组、对象等复杂类型
let obj = ref({ name: 'frank', age: 25 });
console.log(obj.value.name);
const picurl = ref('../../static/logo.png');
function onClick() {
	isActive.value = !isActive.value;
}
const list = ref([
	{ id: 1, name: 'frank', age: 18 },
	{ id: 2, name: 'frank2', age: 19 },
	{ id: 3, name: 'frank3', age: 20 }
]);
// 计算属性，它和方法的区别在于，计算属性具有缓存性，而方法每次调用都会执行
const firstName = ref('');
const lastName = ref('');
// 注意计算属性使用ref来做后续逻辑处理的时候，一定要用.value来取值，它和template中的不一样
const fullName = computed(() => firstName.value + '-' + lastName.value);
// 监听属性并附带一些副作用
watch(firstName, (newValue, oldValue) => {
	console.log(newValue, oldValue);
});
const person = ref({
	name: 'frank',
	age: 18
});
// watch如果监听的是一个对象，那监听的第一个参数要写成箭头函数来指定监听对象的属性
watch(
	() => person.value.name,
	(newValue, oldValue) => {
		console.log(newValue, oldValue);
	}
);
</script>

<style lang="scss">
.box {
	width: 100px;
	height: 100px;
	background: orange;
}
.active {
	background: red;
}
.boxClick {
	width: 200px;
	height: 200px;
	background: green;
}
input {
	border: 1px solid #ccc;
	height: 40px;
	padding: 0 10px;
	margin: 10px 0;
}
</style>
