<template>
	<view>
		<!-- <view class="title1">
			<view style="flex-basis: 48%"></view>
			<view>你好</view>
		</view> -->
		<!-- 上半部分内容 -->
		<view class="top">
			<!-- 头像及用户名 -->
			<view class="avatar-box flex-layout flex-center">
				<u-avatar :src="src" mode="square" size="mini" @click="uspace"></u-avatar>
				<view class="user-name-box">
					<view class="user-name" @click="uspace">{{nickname}}</view>
					<u-tag text="普通会员" size="mini" bg-color="#a9aba6" color="#fff" border-color="transparent"
						shape="circle" />
				</view>
				<u-icon name="setting" label="设置" label-color="white" @click="go_to_set"></u-icon>
			</view>
			<!-- 用户账户等信息 -->
			<!-- <view class="top-grid">
				<u-grid :col="4" :border="false">
							<u-grid-item :key="index" v-for="(item,index) in topGriDdata" bg-color="transparent">
						<view class="thisicon">
					<u-icon size="40" color="#ffffff" :name="item.icon"></u-icon>
						</view>
						<view class="mytext">{{item.text}}</view>
					</u-grid-item>
				</u-grid>
			</view> -->
		</view>
		<!-- 底部白色模块 -->
		<view class="bottom">
			<!-- 我的省钱 -->
			<u-card class="first-card" title="省事秘诀" title-color="#000000" title-size="25" padding="30" margin="30rpx">
				<view class="money" slot="body">
					<u-grid :col="3" :border="false">
						<u-grid-item :key="index" v-for="(item,index) in firstpart" bg-color="transparent"
							@click="go_to_index(item)">
							<view class="first-text">{{item.text}}</view>
						</u-grid-item>
					</u-grid>
				</view>

			</u-card>
			<!-- 小工具 -->
			<u-card class="second-card" title="体验反馈区" title-color="#000000" title-size="25" padding="30" margin="30rpx">
				<view class="tool" slot="body">
					<u-grid :col="3" :border="false">
						<u-grid-item :key="index" v-for="(item,index) in secondpart" bg-color="transparent"
							@click="go_to_index(item)">
							<view class="first-text">{{item.text}}</view>
						</u-grid-item>
					</u-grid>
				</view>

			</u-card>
			<!-- 暖暖服务 -->
			<!-- 		<u-card class="third-card" title="暖暖服务" title-color="#000000" title-size="25" padding="30" margin="30rpx">
			<view class="tool" slot="body">
				<u-grid :col="3" :border="false">
					<u-grid-item :key="index" v-for="(item,index) in thirdpart" bg-color="transparent">
						
						<view class="first-text">{{item.text}}</view>
					</u-grid-item>
				</u-grid>
			</view>
			
		</u-card>
	 -->
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				src: uni.getStorageSync('avatar') || '/static/member.png',
				nickname: uni.getStorageSync('nickname') || '请登录账户',
				topGriDdata: [{
						text: '订单',
						icon: '/static/1.png',
						url: ''
					},
					{
						text: '钱包',
						icon: '/static/2.png',
						url: ''
					},
					{
						text: '帮助',
						icon: '/static/3.png',
						url: ''
					},
					{
						text: '设置',
						icon: '/static/4.png',
						url: ''
					},
				],
				firstpart: [{
						text: '领卷中心',
						icon: '',
						url: '../coupon/coupon'
					},
					{
						text: '公众号',
						icon: '',
						url: ''
					},
					{
						text: '邀请有礼',
						icon: '',
						url: '../invite/invite'
					}


				],
				secondpart: [{
						text: '在线客服',
						icon: '',
						url: ''
					},
					{
						text: '常见问题',
						icon: '',
						url: '../customer_service/customer_service'
					},
					{
						text: '意见反馈',
						icon: '',
						url: ''
					},
					{
						text: '超值长租',
						icon: '',
						url: '../long_rent/long_rent'
					},
				],
				thirdpart: [{
						text: '咘咘商城',
						icon: '',
						url: ''
					},
					{
						text: '违章查看',
						icon: '',
						url: ''
					},
					{
						text: '新手指引',
						icon: '',
						url: '../guide/guide'
					},
					{
						text: '帮助',
						icon: '/static/3.png',
						url: ''
					}
				]

			}

		},
		methods: {
			uspace() {

			},
			vip() {

			},
			go_to_index(place) {
				if (place.text == '常见问题') {
					uni.switchTab({
						url: '../customer_service/customer_service'
					})
				} else {
					uni.navigateTo({
						url: place.url
					})
				}
			},
			go_to_set() {
				uni.navigateTo({
					url: './setting'
				})
			}
		},
		onLoad() {
			if ((this.avatar == '/static/member.png') || (this.nickname == '请登录账户')) {
				var mobile = uni.getStorageSync('mobile')
				uniCloud.callFunction({
					name: "user-center",
					data: {
						action: "wode",
						mobile: mobile
					}
				}).then(res => {
					if (res.result.data.length == 0) {
						uni.showToast({
							title: "获取昵称与头像失败，请重新登录",
							icon: "error"
						})
					} else {
						this.src = res.result.data[0].avatar
						uni.setStorageSync('avatar', this.src)
						console.log("cloudfunction", this.src)
					}
				})
			}
		}
	}
</script>

<style>
	/* .title1{
		display:flex;
		top:0rpx;
		height:100rpx;
		position: fixed;
		background-color: #ff5500;
		color:#FFFFFF;
		width: 100%;
	} */

	.top {
		background-color: #ff5500;
		height: 250rpx;
		/* margin-top:100rpx */
	}

	.avatar-box {
		padding: 15px;
		color: #ffffff;
		display: flex;
		/* flex-direction: row; */
	}

	.avatar-box .user-name-box {
		flex: 1;
		padding: 0 25rpx;
	}

	.avatar-box .user-name {
		font-size: 30rpx;
		font-weight: bolder;
		margin-bottom: 15rpx;
	}

	.top-grid {
		padding-bottom: 20rpx;
		margin-bottom: 25rpx;
	}

	.top-grid .thisicon {
		color: #ffffff;
	}

	.top-grid .mytext {
		color: #ffffff;
		font-size: 20rpx;
		margin-top: 8rpx;

	}

	.bottom {
		min-height: 1000rpx;
		background-color: #f8f8f8;
		position: relative;
		top: -65rpx;
		border-radius: 40rpx 40rpx 0 0;

	}

	.first-text {
		color: #000000;
		font-size: 22rpx;
		margin-top: 10rpx;
	}
</style>
