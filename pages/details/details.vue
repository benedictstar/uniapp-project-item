<template>
	<view>
		<view class="nav">
			<u-navbar back-text="" title="订单详情" :background="navbarbgc"title-color="#fff" :b:background="navbarbgc"order-bottom="false" title-size="30">
				<view class="u-flex u-row-right" style="width: 100%; ">
					<u-icon class="u-m-r-30" name="kefu-ermai" color="#FFFFFF" size="48"></u-icon>
					<u-icon class="u-m-r-30" name="more-dot-fill" color="#ffffff" size="48"></u-icon>
				</view>
			</u-navbar>

			<steps_new class="u-p-16 u-p-t-30 u-p-b-80 " :list="stepList" :current="1" mode="number" active-color="#FFFFFF"></steps_new>
		</view>

		<view class="content u-p-l-20 u-p-r-20" style="position: relative; top: -280rpx;" >
			<view class="u-p-t-20" >
				<u-cell-group>
					<view class="u-flex u-border-bottom">
						<u-image class="u-p-26" width="35%" height="200rpx" :src="src"></u-image>
						<view>
							<view class="u-font-40">{{carDetails.brand}}</view>
							<view style="color:#9493a1">{{carDetails.license_number}}</view>
							<view style="color:#9493a1">日均行驶{{carDetails.car_km}}km</view>
						</view>
					</view>
					<!-- <view class="u-flex u-row-between">
						<view class="u-p-26" style="color:#9493a1">
							<view>7月2日 21:00</view>
							<view class="u-p-l-26">租客自取</view>
						</view>
						<view style="color:#9493a1">1天</view>
						<view class="u-p-26" style="color:#9493a1">
							<view>7月2日 21:00</view>
							<view class="u-p-r-26 u-text-right">租客自还</view>
						</view>
					</view> -->
					<view class="time-box" style="display: flex; justify-content: space-around;">
						<view class="day-box"style="padding-top:30px;margin-left: 10rpx;">
						<view class="day" style="font-size: 25rpx;color: #686967;">共{{carDetails.day}}天</view>
						</view>
						<view class="color-block" style="background-color:#E35C31;width: 20rpx;height: 100rpx;margin-top:13px;"></view>
						<view class="right-box" style="display: flex;justify-content: space-between;">
							<view class="detail-time-box" style="padding-top: 30rpx; padding-right: 50rpx;padding-top: 40rpx; letter-spacing: 1rpx;font-size: 15rpx;color: #696867;">
								<view class="star-time"style="padding-bottom: 20rpx;">{{carDetails.submit_time}}</view>
								<view class="end-time">{{carDetails.back_time}}</view>
							</view>
							
							<view class="take-way"style="padding-top: 40rpx;margin-right: 30rpx;font-size: 15rpx;color: #696867;">
								<view class="star-takeway"style="padding-bottom: 20rpx;">{{carDetails.submit_way}}</view>
								<view class="end-takeway">{{carDetails.back_way}}</view>
							</view>
						</view>
					</view>
					<u-cell-item icon="map" title="取车点" :label="carDetails.submit_address"></u-cell-item>
					<u-cell-item icon="map" title="还车点" :label="carDetails.back_address"></u-cell-item>
					<u-cell-item icon="account" :title="carDetails.ownername" label="车主" :arrow="false">
						<u-icon class="u-m-r-30" name="chat" size="48" slot="right-icon"></u-icon>
						<u-icon class="u-m-r-8" name="phone" size="48" slot="right-icon"></u-icon>
					</u-cell-item>
				</u-cell-group>
			</view>
			<view class="u-p-t-20">
				<u-cell-group>
					<u-cell-item style="font-weight:700" title="费用明细" @click="toCostDetails"></u-cell-item>
					<u-cell-item title="租车费用">{{carDetails.total_fee}}元</u-cell-item>
					<u-cell-item title="车辆押金">{{carDetails.deposit}}元</u-cell-item>
					<u-cell-item title="违章押金" value="2000元"></u-cell-item>
				</u-cell-group>
			</view>
			<view class="u-p-t-20">
				<u-cell-group style="font-weight: 700;">
					<u-cell-item title="给车主补钱" @click="toCompensation"></u-cell-item>
					<u-cell-item title="交接车照片"@click="toHandoverCarPic" ></u-cell-item>
					<u-cell-item title="交接车指南" @click="toHandoverCarGuide"></u-cell-item>
				</u-cell-group>
			</view>
			<view class="u-p-t-20">
				<u-cell-group style="font-weight: 700;">
					<u-cell-item @click="toAccidentCompensation" title="出事故理赔"></u-cell-item>
					<u-cell-item @click="toPeccancyInfo" title="违章查询"></u-cell-item>
					<u-cell-item @click="toCarUseGuide" title="车辆使用指南"></u-cell-item>
				</u-cell-group>
			</view>
			<view class="u-p-t-20">
				<u-cell-group>
					<u-cell-item title="订单编号" :value="orderID" :arrow="false">
						<view @click="copy(orderID)" slot="right-icon" class="u-p-l-15" style="color:#E35C31">复制</view>
					</u-cell-item>
					<u-cell-item title="下单时间" :value="carDetails.create_time" :arrow="false"></u-cell-item>
				</u-cell-group>
			</view>
			<view class="u-m-t-20 u-p-t-20 u-p-b-40 u-flex" style="background-color: #fff">
				<u-button hover-class="none" :plain="true"  shape="circle">修改订单</u-button>
				<u-button type="success" shape="circle" style="background-color: #E35C31">联系客服</u-button>
			</view>
		</view>
	</view>
</template>

<script>
import steps_new from '../../components/step-news/step-news.vue'
export default {
	data() {
		return {
			orderID: '9959 0220 7012 99',
			src: 'https://carphoto.atzuche.com/2car/20/07/965386993/1595570702454_1.jpg',
			navbarbgc: {
				backgroundColor: '#41444c'
			},
			carDetails:{
				brand:'宝马',
				license_number:'粤123123123',
				car_km:'200',
				day:'1',
				submit_time:'2020年9月19日20:00',
				back_time:'2020年9月20日20:00',
				submit_address:'东南亚芒果',
				back_address:'泰国芒果',
				ownername:'黎子聪',
				submit_way:'客户自取',
				back_way:'客户自还',
				total_fee:'100000',
				deposit:'2000',
				create_time:'2021年12月20日 13:41:23'
			},
			stepList: [
				{
					name: '支付费用'
				},
				{
					name: '支付押金'
				},
				{
					name: '取车'
				},
				{
					name: '用车'
				},
				{
					name: '还车'
				},
				{
					name: '订单完成'
				}
			]
		};
	},
	components:{
		steps_new
	},
	methods: {
		copy(value) {
			uni.setClipboardData({
				data: value, //要被复制的内容
				success: function() {
					uni.showToast({
						title: '复制成功',
						duration: 1000,
						icon: 'none'
					});
				},
				fail: function(err) {
					uni.showToast({
						title: '复制失败',
						duration: 1000,
						icon: 'none'
					});
				}
			});
		},
		toCostDetails() {
			uni.navigateTo({
				url: '/pages/sure_order/fare'
			});
		},
		toCompensation() {
			uni.navigateTo({
				url: '/pages/details/compensation'
			});
		},
		toHandoverCarPic(){
			uni.navigateTo({
				url: '/pages/details/handoverCarPic'
			});
		},
		toCarUseGuide(){
			uni.navigateTo({
				url: '/pages/details/carUseGuide'
			});
		},
		toHandoverCarGuide(){
			uni.navigateTo({
				url: '/pages/details/handoverCarGuide'
			});
		},
		toPeccancyInfo(){
			uni.navigateTo({
				url: '/pages/details/peccancyInfo'
			});
		},
		toAccidentCompensation(){
			uni.navigateTo({
				url: '/pages/details/accidentCompensation'
			});
		}
	}
};
</script>

<style scoped lang="scss">
	page{
		background-color: #F5F2f2
	}
.nav {
	background-color: #E35C31;
	border: 1rpx solid #E35C31;
	height: 500rpx;
	border-radius: 30rpx;
	u-navbar {
		view {
			display: flex;
			justify-content: flex-end;
			// background-color: #E35C31;
		}
	}
}
.content {
	// background-color: #f5f5f5;
}
.nav /deep/ .u-navbar-inner{
	background-color:#E35C31
}
// .nav /deep/ .u-icon__icon{
// 	background-color:#E35C31;
// }
.content /deep/ .u-cell-item-box{
	
	border-radius: 50rpx;
}


</style>
