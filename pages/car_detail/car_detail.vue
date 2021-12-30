<template>
	<!-- <view class="scol">
		<view class="main">
			<view class="map">
				放置地图轮播图
				<swiper :autoplay="autoplay" :interval="interval" :indicator-dots="indicatordots"
					style="width: 750rpx;height:380rpx">
					<swiper-item v-for="(item,index) in ima" :key="index">
						<image :src="item.src" style="width: 750rpx;height:400rpx"></image>
					</swiper-item>
				</swiper>
			</view>
			<view class="details">
				价格，车辆名称、等信息
				<view class="money">
					<text class="money1">￥{{rmb}}</text>
					<text class="money2">/天</text>
				</view>
				车辆信息
				<view class="car">
					<text space="nbsp">{{car}} {{type}} {{patten}}</text>
					<view class="times">
						<text>已被青睐101次</text>
					</view>
				</view>
				<view class="basicinf">
					<u-row gutter="8">
						<u-col span="3">
							<u-tag :text="pnumber" size="mini" bg-color="#ff5500" color="#ffffff"
								border-color="transparent" shape="circle" />
						</u-col>
						<u-col span="4">
							<u-tag text="日均限300km" size="mini" bg-color="#ff5500" color="#ffffff"
								border-color="transparent" shape="circle" />
						</u-col>
					</u-row>
				</view>
				<view>
					<u-card class="basic" title="基本配置" title-color="#000000" title-size="25" margin="30rpx"
						:head-border-bottom="true">
						<u-grid :border="false" :col="2" slot="body">
							<u-grid-item v-for="(item,index) in binf" :key="index" bg-color="transparent">
								<view class="inf">{{item.text}}</view>
							</u-grid-item>
						</u-grid>
					</u-card>
					<u-card title="车况信息" title-color="#000000" title-size="25" margin="30rpx">
						<u-grid :border="false" slot="body" :col="1">
							<u-grid-item>
								<view class="sinf">近期该车辆未更新检测信息</view>
							</u-grid-item>
						</u-grid>
					</u-card>
					<u-card title="车辆位置" title-color="#000000" title-size="25" margin-top="30rpx">
						<u-grid :border="false" slot="body" :col="1">
							<u-grid-item>
								<u-icon name="map" :label="place" label-color="#4690d5" color="#4690d5" @click="jump">
								</u-icon>
							</u-grid-item>
						</u-grid>
					</u-card>
				</view>
			</view>
		</view>
		<view @click="go_to_sure_order">
			<bottom3></bottom3>
		</view>
	</view> -->
	<view class="scol">
		<view class="main">
			<view class="map">
				<view style="position: relative;margin-bottom:-70rpx;margin-top:30rpx;z-index: 9999;"><u-icon size="36" name="arrow-left" @click="back"></u-icon></view>
				<u-swiper :list="ima" height=550 :autoplay="false" style="border-top-left-radius:150rpx;z-index: 1;position: relative;"></u-swiper>
			</view>
			<view class="details">
				<!-- 价格，车辆名称、等信息 -->
				<view class="money">
					<text class="money1">￥{{rmb}}</text>
					<text class="money2">/天</text>
				</view>
				<!-- 车辆信息 -->
				<view class="car">
					<text space="nbsp">{{car}}{{type}}  {{patten}}</text>
				</view>
				<view class="basicinf">
						<u-icon name="map" :label="place" label-color="#474747" color="#474747" @click="jump"></u-icon>
				</view>
				<view>
					<view class="mid">
						<u-grid :border="false" :col="4">
							<u-grid-item v-for="(item,index) in binf" :key="index" bg-color="transparent">
								<view class="inf2">{{item.dis}}</view>
								<view class="inf">{{item.text}}</view>
							</u-grid-item>
						</u-grid>
					</view>
					<u-card :border="false" title="车况信息" title-color="#000000" title-size="25" margin="30rpx">
						<u-grid :border="false" slot="body" :col="1" >
							<u-grid-item>
								<view class="sinf">近期该车辆未更新检测信息</view>
							</u-grid-item>
						</u-grid>
					</u-card>
				</view>
			</view>
		</view>
		<view @click="go_to_sure_order">
			<bottom3></bottom3>
		</view>
	</view>
</template>

<script>
	import bottom3 from '../../components/bottom3.vue'
	export default {
		data() {
			return {
				// 图片存放处
				ima:[
					{image:'/static/car.png'},
					{image:'/static/car.png'},
					{image:'/static/car.png'},
				],
				//轮播图参数控制
				src: '/static/1.jfif',
				indicatordots: true,
				autoplay: false,
				interval: 2000,
				//页面配置后端交接参数
				rmb: 500,
				car: '保时捷',
				type: 'S1',
				patten: '2021款',
				pnumber: '粤A12345',
				binf:[
					{text:"自动档",dis:"AT"},
					{text:"油耗",dis:"2.0L"},
					{text:"车龄",dis:"1"},
					{text:"车座",dis:"4"},
					],
				place: '广东省华南理工大学大学城校区'
			}
		},
		components: {
			bottom3
		},
		methods: {
			jump() {
				var textObj = JSON.stringify(this.place)
				uni.navigateTo({
					url: './map?place=' + textObj
				})
			},
			go_to_sure_order() {
				uni.navigateTo({
					url: '../sure_order/sure_order'
				})
			},
			back(){
				uni.navigateBack({
				})
			}
			

		},
		onLoad() {
			console.log("onload")
			//调用云函数获取车辆信息
			uniCloud.callFunction({
					name: "car-center",
					data: {
						action: "search",
						_id:"79550af260e95cb425a37b9808e1488d"
					}
				})
				.then(res => {
					console.log(res)
					this.car = res.result.data[0].brank
					this.rmb = res.result.data[0].price
					this.type = res.result.data[0].name
					this.patten = res.result.data[0].year_type
					this.pnumber = res.result.data[0].license_number
					this.binf[0].text = res.result.data[0].car_gear
					this.binf[1].text = res.result.data[0].car_age+"年"
					this.binf[2].text = res.result.data[0].fuel_tank
					this.binf[3].text = res.result.data[0].car_seat
					this.ima = res.result.data[0].car_imgs
					this.place = res.result.data[0].deliver_address
				})
		}

	}
</script>

<style lang="scss">
	// .scol {

	// 	//   width: 100%;
	// 	//   height:100%;
	// 	// display: flex;
	// 	// flex:1;
	// 	// height:1300rpx;
	// }

	// .main {
	// 	display: flex;
	// 	flex-direction: column;
	// 	width: 100%;
	// 	height: 1200rpx;

	// }

	// .map {
	// 	height: 400rpx;
	// 	width: 100%;
	// }

	// .details {
	// 	// min-height: 1200rpx;
	// 	background-color: #f8f8f8;
	// 	margin-bottom: 80rpx;
	// }

	// .details .money {
	// 	margin-top: 20rpx;
	// 	margin-left: 25rpx;
	// }

	// .details .money .money1 {
	// 	font-size: 40rpx;
	// 	font-weight: bold
	// }

	// .details .money .money2 {
	// 	font-size: 20rpx;
	// }

	// .details .car {
	// 	margin-top: 20rpx;
	// 	margin-left: 25rpx;
	// 	font-size: 38rpx;
	// 	font-weight: bold
	// }

	// .basicinf {
	// 	font-size: 25rpx;
	// 	margin-top: 20rpx;
	// 	margin-left: 25rpx;
	// }

	// .basic .inf {
	// 	text-align: left;
	// 	font-size: 20rpx;
	// 	font-weight: bold;

	// }
	.scol{
		
		//   width: 100%;
		//   height:100%;
		// display: flex;
		// flex:1;
		// height:1300rpx;
		// background-color:#f94f00 ;
	}
	.main{
		display:flex;
		flex-direction: column;
		width:100%;
		// background-color:#f94f00 ;
		// border-top-left-radius:100rpx;
		// height:1800rpx;
		background-color:#f94f00 ;
		
		
	}
	.map{
		// height:400rpx;
		width:100%;
		background-color:white;
		// margin-top:100rpx
	}
	.details{
		// min-height: 1200rpx;
		background-color: #f94f00;
		margin-bottom:80rpx;
	}
	.details .money{
		margin-top:20rpx;
		margin-left:25rpx;
	}
	.details .money .money1{
		font-size:50rpx;
		font-weight:bold;
		color:white
	}
	.details .money .money2{
		font-size:30rpx;
		color:white
	}
	.details .car{
		margin-top:20rpx;
		margin-left:25rpx;
		font-size:38rpx;
		font-weight:bold
		
	}
	.basicinf{
		font-size: 25rpx;
		margin-top:20rpx;
		margin-left:25rpx;
	}
	.inf{
		text-align: left;
		font-size: 25rpx;
		// font-weight: bold;
		
	}
	.inf2{
		text-align: left;
		font-size: 40rpx;
		font-weight: bold;
		
	}
	.mid{
		margin:30rpx;
		background-color: white;
		border-radius:15rpx
	}

	// .bottom1{
	// 	background:#ff5500;
	// 	  color: #ffffff;
	// 	  height: 100%;
	// 	  position:fixed;
	// 	  width:40%;
	// 	  margin-left:40%;
	// 	  margin-right: 20%;
	// 	  border-radius: 40rpx 40rpx 0 0;
	// }
	/* .details .car .times{
			text-align:right;
			font-size: 22rpx;
	} */
</style>
