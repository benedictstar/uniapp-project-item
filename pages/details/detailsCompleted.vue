<!-- 已完成订单详情 -->
<template>
	<view>
		<view class="nav ">
			<u-navbar back-text="" title="订单详情" :background="navbarbgc" title-color="#fff" :border-bottom="false" title-size="28">
				<view class="u-flex u-row-right" style="width: 100%;">
					<u-icon class="u-m-r-30" name="kefu-ermai" color="#fff" size="48"></u-icon>
					<u-icon class="u-m-r-30" name="more-dot-fill" color="#fff" size="48"></u-icon>
				</view>
			</u-navbar>

			<u-steps class="u-p-16 u-p-t-30 u-p-b-80 " :list="stepList" :current="5" mode="number" active-color="#42b983"></u-steps>
		</view>

		<view class="content u-p-l-20 u-p-r-20">
			<view class="u-p-t-20">
				<u-cell-group>
					<u-cell-item icon="account" title="Mr.孔" label="车主" :arrow="false">
						<u-icon class="u-m-r-30" name="chat" size="48" slot="right-icon"></u-icon>
						<u-icon class="u-m-r-8" name="phone" size="48" slot="right-icon"></u-icon>
					</u-cell-item>
					<view class="u-flex u-border-bottom">
						<u-image class="u-p-26" width="35%" height="200rpx" :src="src"></u-image>
						<view>
							<view class="u-font-40">迈凯伦650S 3.8T</view>
							<view style="color:#9493a1">沪D***51</view>
							<view style="color:#9493a1">日均限200km</view>
						</view>
					</view>
					<view class="u-flex u-row-between">
						<view class="u-p-26" style="color:#9493a1">
							<view>7月2日 21:00</view>
							<view class="u-p-l-26">租客自取</view>
						</view>
						<view style="color:#9493a1">1天</view>
						<view class="u-p-26" style="color:#9493a1">
							<view>7月2日 21:00</view>
							<view class="u-p-r-26 u-text-right">租客自还</view>
						</view>
					</view>
					<u-cell-item icon="map" title="自取" label="广州市番禺区小谷围街道华南理工大学"></u-cell-item>
					<u-cell-item icon="map" title="自还" label="广州市番禺区小谷围街道华南理工大学"></u-cell-item>
				</u-cell-group>
			</view>
			<view class="u-p-t-20">
				<u-cell-group>
					<u-cell-item style="font-weight:700" title="费用明细" @click="toCostDetails"></u-cell-item>
					<u-cell-item title="租车费用" value="509元"></u-cell-item>
					<u-cell-item title="车辆押金" value="2000元"></u-cell-item>
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
									<u-cell-item title="驾驶员身份信息" @click="toDriverInfo"></u-cell-item>
				</u-cell-group>
			</view>
			<view class="u-p-t-20">
				<u-cell-group>
					<u-cell-item title="订单编号" :value="orderID" :arrow="false">
						<view @click="copy(orderID)" slot="right-icon" class="u-p-l-15" style="color:#18B566">复制</view>
					</u-cell-item>
					<u-cell-item title="下单时间" value="2021年7月2日 13:41:37" :arrow="false"></u-cell-item>
				</u-cell-group>
			</view>
			<view class="u-m-t-20 u-p-t-20 u-p-b-40 u-flex" style="background-color: #fff">
				<u-button hover-class="none" :plain="true"  shape="circle">联系车主</u-button>
				<u-button type="success" shape="circle">再次预定</u-button>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			orderID: '9959 0220 7012 99',
			src: 'https://carphoto.atzuche.com/2car/20/07/965386993/1595570702454_1.jpg',
			navbarbgc: {
				backgroundColor: '#41444c'
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
				url: '/pages/details/costDetails'
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
		},
		toDriverInfo(){
			uni.navigateTo({
				url: '/pages/details/driverInfo'
			});
		}
	}
};
</script>

<style scoped lang="scss">
.nav {
	background-color: #41444c;
	u-navbar {
		view {
			display: flex;
			justify-content: flex-end;
		}
	}
}
.content {
	background-color: #f5f5f5;
}

</style>
