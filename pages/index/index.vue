<template>
	<navigator url="/pages/requestDemo/requestDemo">跳转到requestDemo</navigator>
	<!--组件中定义好的参数名称传递参数-->
	<!--子传父，需要通过emit传递的函数名称和接收参数-->
	<UserInfo username="frank"></UserInfo>
	<UserInfo username="frank123" @add="onAdd" @change="onChange"></UserInfo>
	<UserInfo @add="onAdd" @change="onChange"></UserInfo>
	<!--通过defineExpose获取属性-->
	<demo-child ref="child"></demo-child>
	<button @click="update">defineExpose更新</button>
	<view>{{ child }}</view>
	<view>
		{{ emitRandom }}
	</view>
	<view class="box" hover-class="boxHover">
		<view class="inner" hover-class="innerHover" hover-stop-propagation>内部元素</view>
	</view>
	<navigator url="/pages/demo1/demo1">跳转</navigator>
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
import { ref, onMounted } from 'vue';
import { onHide, onShow } from '@dcloudio/uni-app';
let emitRandom = ref(0);
const onAdd = function (e) {
	console.log(e);
};
uni.showToast({
	title: 'test toast'
});

// 设置本地缓存（支持同步和异步）
uni.setStorageSync('key', 'value');

function onChange(e) {
	console.log(e);
	emitRandom.value = e;
}
// 注意这里创建的对象名称要和引入的组件ref属性保持一致
const child = ref(null);
onMounted(() => {
	console.log(child.value);
});
// 这个调用可以不用结合生命周期函数，因为能触发click事件一定是DOM已经渲染完成后
const update = function () {
	child.value.updateCount();
};
// 页面生命周期
onHide(() => {
	console.log('触发onHide');
});
onShow(() => {
	console.log('触发onShow');
});
</script>

<style lang="scss">
.box {
	width: 200px;
	height: 200px;
	background: #ccc;
}
.boxHover {
	background: orange;
	width: 300px;
}
.inner {
	width: 150px;
	height: 150px;
	background: green;
}
.innerHover {
	background: greenyellow;
}
.scrollView {
	width: 80%;
	height: 220px;
	border: 1px solid red;
	// 不允许换行
	white-space: nowrap;
	.scrollBox {
		width: 100px;
		height: 100px;
		background: green;
		// 块横向排列
		display: inline-block;
	}
}
</style>
