<!-- 违章信息 -->
<template>
	<view>
		<view class="nav"><u-navbar title="违章信息" title-color="#000" :title-bold="true"></u-navbar></view>
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
					name: '待处理'
				},
				{
					name: '已完成'
				}
			]
		};
	},
	methods: {}
};
</script>

<style></style>
