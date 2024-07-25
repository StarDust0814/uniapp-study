<template>
	<view class="layout">{{ arrs }}</view>
</template>

<script setup>
let arrs = ref([]);
function request() {
	uni.request({
		url: 'https://jsonplaceholder.typicode.com/posts',
		success: (res) => {
			console.log(res);
			arrs.value = res.data;
		}
	});
}
request();
</script>

<style lang="scss" scoped></style>
