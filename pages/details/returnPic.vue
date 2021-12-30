<template>
	<view class="wrap u-p-26">
		<view class="nav"><u-navbar title="还车照片" title-color="#000" :title-bold="true"></u-navbar></view>
		<u-sticky bg-color="#fff" style="color:#a19ea6">
			<!-- 只能有一个根元素 -->
			<view class="sticky u-flex u-col-center u-font-12" style="height:100rpx">取还车时要对完整的车身外观特别是损伤处（如划痕、轮胎、轮毂）及当前里程数与油量进行拍照</view>
		</u-sticky>
		<view class="u-flex">
			<u-upload upload-text="正面照" max-count="1" :multiple="false" width="220" height="220"></u-upload>
			<u-upload upload-text="背面照" max-count="1" :multiple="false" width="220" height="220"></u-upload>
			<u-upload upload-text="左侧照" max-count="1" :multiple="false" width="220" height="220"></u-upload>
		</view>
		<view class="u-flex">
			<u-upload upload-text="右侧照" max-count="1" :multiple="false" width="220" height="220"></u-upload>
			<u-upload upload-text="仪表盘" max-count="1" :multiple="false" width="220" height="220"></u-upload>
			<u-upload upload-text="更多照片" max-count="1" :multiple="false" width="220" height="220"></u-upload>
		</view>
		<view class="u-p-26"><u-button type="success" shape="circle">上传</u-button></view>
	</view>
</template>

<script>
export default {
	data() {
		return {};
	},
	methods: {}
};
</script>

<style></style>
