<!-- 筛选页面 -->
<template>
	<view class="u-p-26">
		<u-navbar back-text="" title="筛选" title-color="#000"></u-navbar>
		<view v-for="(item, index) in filter" v-if="index >= 1">
			<view class="title">{{ item.groupName }}</view>
			<view class="content u-flex u-flex-wrap ">
				<view class="tag" @click="filterCheck(item2)" :class="{ active: item2.checked }" v-for="(item2, index2) in item.groupContent">{{ item2.name }}</view>
			</view>
		</view>

		<view class="u-m-t-20 u-p-t-20 u-p-b-40 u-flex" style="background-color: #fff">
			<u-button @click="clear" :plain="true" shape="circle">清空</u-button>
			<u-button @click="ack" type="success" shape="circle" style="width:70%">确定</u-button>
		</view>
	</view>
</template>

<script>
export default {
	onLoad() {
		this.filter = getApp().globalData.filter;
		this.filterNames = getApp().globalData.filterNames;
	},
	data() {
		return {
			filterNames: [],
			filter: []
		};
	},
	onShow()
	{
		let other_condition = getApp().globalData.filter[0];
		let license = getApp().globalData.filter[2];
		let limited = getApp().globalData.filter[4];
		// 筛选页面返回到这里时刷新数据
		if(other_condition.groupContent[2].checked)
		{			
			license.groupContent[0].checked = true;			
		}else{
			license.groupContent[0].checked = false;			
		}
		if(other_condition.groupContent[3].checked)
		{			
			limited.groupContent[0].checked=true;			
		}
		else{
			limited.groupContent[0].checked=false;
		}
	},
	methods: {
		filterCheck(item2) {
			if (item2.checked === false) {
				this.filterNames.push(item2.name);
				
			} else {
				let idx = this.filterNames.indexOf(item2.name);
				this.filterNames.splice(idx, 1);				
			}
			item2.checked = !item2.checked;
		},
		clear() {
			//清空filter数组
			for (const item of this.filter) {
				for (const item2 of item.groupContent) {
					item2.checked = false;
				}
			}
			//重置fulterNames数组
			let flag1 = false;
			let flag2 = false;
			if (this.filterNames.includes('特价车')) {
				flag1 = true;
			}
			if (this.filterNames.includes('严选优车')) {
				flag2 = true;
			}
			if (flag1 && flag2) {
				this.filterNames = ['特价车', '严选优车'];
			} else if (flag1) {
				this.filterNames = ['特价车'];
			} else if (flag2) {
				this.filterNames = ['严选优车'];
			} else {
				this.filterNames = [];
			}
		},
		ack() {
			getApp().globalData.filter = this.filter;
			getApp().globalData.filterNames = this.filterNames;
			uni.navigateTo({
				url: '/pages/carList/carList'
			});
			
		}
	}
};
</script>

<style>
.title {
	font-size: 35rpx;
	margin-bottom: 25rpx;
}
.tag {
	font-size: 25rpx;
	background-color: #f6f6f6;
	width: 30%;
	height: 70rpx;
	text-align: center;
	line-height: 70rpx;
	border-radius: 25rpx;
	margin-right: 15rpx;
	margin-top: 15rpx;
	margin-bottom: 15rpx;
}
.active {
	background-color: orange;
	color: #fff;
}
</style>
