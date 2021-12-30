<!-- 交接车指南 -->
<template>
	<view>
		<view class="nav"><u-navbar title="交接车指南" title-color="#000" :title-bold="true"></u-navbar></view>
		<u-tabs-swiper active-color="green" ref="tabs" :list="list" :is-scroll="false"></u-tabs-swiper>
		<!-- 待完善 -->
	</view>
</template>

<script>
export default {
	data() {
		return {
			list: [
				{
					name: '车管家上门'
				}
			]
		};
	},
	methods: {}
};
</script>

<style></style>
