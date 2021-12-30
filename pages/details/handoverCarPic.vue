<!-- 交接车拍照 -->
<template>
	<view>
		<view class="nav"><u-navbar height="85" back-text="返回" title="交接车拍照" title-color="#000" :title-bold="true"></u-navbar></view>
		<view class="content" style="background-color:#f5f2f5">
			<u-cell-group title="请在交接车辆时,按照提示上传车辆照片" :title-style="{ 'font-size': '26rpx' }">
				<u-cell-item @click="toPickupPic" title="取车照片" value="待完善" :title-style="{ 'font-weight': '600' }"></u-cell-item>
				<u-cell-item @click="toReturnPic" title="还车照片" value="待完善" :title-style="{ 'font-weight': '600' }"></u-cell-item>
			</u-cell-group>
			<u-cell-group class="u-p-t-26" title="交接车需知" :title-style="{ 'font-size': '26rpx' }">
				<u-cell-item @click="toOilCost" title="交接车油费计算方式" :title-style="{ 'font-weight': '600' }"></u-cell-item>
				<u-cell-item @click="toExceptionHandling" title="交接车意外情况处理流程" :title-style="{ 'font-weight': '600' }"></u-cell-item>
			</u-cell-group>
			<u-cell-group class="u-p-b-26" title="车辆使用指南" :title-style="{ 'font-size': '26rpx' }">
				<u-cell-item @click="toCarUseGuide" title="车辆使用指南" :title-style="{ 'font-weight': '600' }"></u-cell-item>
			</u-cell-group>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {};
	},
	methods: {
		toPickupPic() {
			uni.navigateTo({
				url: '/pages/details/pickupPic'
			});
		},
		toReturnPic() {
			uni.navigateTo({
				url: '/pages/details/returnPic'
			});
		},
		toOilCost() {
			uni.navigateTo({
				url: '/pages/details/oilCost'
			});
		},
		toExceptionHandling() {
			uni.navigateTo({
				url: '/pages/details/exceptionHandling'
			});
		},
		toCarUseGuide(){
			uni.navigateTo({
				url: '/pages/details/carUseGuide'
			});
		}
	}
};
</script>

<style>
page {
	background-color: #f5f2f5;
}
</style>
