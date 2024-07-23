<template>
	<view>子组件</view>
</template>

<script setup>
import { ref } from 'vue';
const count = ref(100);
const updateCount = function () {
	count.value++;
};
defineExpose({
	count,
	updateCount
});
</script>

<style lang="scss"></style>
