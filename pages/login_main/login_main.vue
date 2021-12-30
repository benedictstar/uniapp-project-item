

<template>
	<view>
		<view class="" style="font-size: 60rpx; font-weight: 700; width: 90%; margin: 0 auto;">
			请输入手机号码
		</view>
		<view class="" style="font-size: 10rpx; color: #999; width: 90%; margin: 0 auto;">
			为了方便联系，请输入您的常用手机号码
		</view>
		<input type="text" v-model:value="phone"
			style="border-bottom: 1rpx #999 solid;line-height: 100rpx; width: 90%; margin: 0 auto; height: 100rpx;margin-top: 50rpx;"
			placeholder="请输入手机号" />
		<view class="" @click="submit"
			style="font-size: 30rpx; width: 80%; margin: 0 auto;height: 80rpx;text-align: center; line-height: 80rpx; background-color: orange; color: white; margin-top: 50rpx;">
			下一步
		</view>
		<view class="" style="width: 100%; margin-top: 300rpx; height: 10rpx; border-top: 2rpx solid #999;">
		</view>
		<div class="" style="float: left; position: relative; left: 50%;top: -30rpx; ">
			<div class="" style="position: relative; left: -50%;background-color: white;padding: 3rpx;">一键登录</div>
		</div>
		<view class="" style="width: 100%; margin-top: 20rpx;">
			<view class="" style="display: flex; justify-content: space-between; width: 80%; margin: 0 auto;">
				<view class="" style="width: 33%;">
					<image class="img" @click="wxlogin" src="../../static/wxlogin.png" mode=""></image>
					<view class="" style="">
						微信登录
					</view>
				</view>
				<view class="" style="width: 33%;">
					<image class="img" @click="aliopenlogin" src="../../static/alpenlog.png" mode=""></image>
					<view class="">
						支付宝登录
					</view>
				</view>
				<view class="" style="width: 33%;">
					<image class="img" @click="not_verification" src="../../static/QQ.png" mode=""></image>
					<view class="">
						免验证
					</view>
				</view>
			</view>
		</view>

		<!-- 一键登录 -->
		<u-popup v-model="show_login_one" mode="bottom">
			<view style="width: 750rpx;margin: 0 auto;border-top-left-radius: 5rpx; border-top-right-radius: 5rpx; ">
				<view class="" style="float: right;" @click="delete_toast">
					×
				</view>
				<view class=""
					style="margin: 0 auto; width: 70%; text-align: center;margin-top: 30rpx; font-size: 50rpx; font-weight: 700;">
					12132131231
				</view>
				<view class="" @click="one_login"
					style="margin: 0 auto; width: 80%; background-color: orange; text-align: center; height: 60rpx;margin-top: 30rpx; font-size: 40rpx; color: white; line-height: 60rpx;border-radius: 30rpx;">
					本机号码一键登录
				</view>
				<view class="" @click="other_login"
					style="margin: 0 auto; width: 80%;  text-align: center; height: 60rpx;margin-top: 30rpx; font-size: 40rpx; line-height: 60rpx;">
					其他登录方式
				</view>
				<label @click="change_checked">
					<view class="" style="padding-bottom: 40rpx;margin-top: 30rpx;">
						<radio style="transform:scale(0.7)" color="#ff5500" :checked="checked_one_login" />
						我已阅读并同意 <text class="" style="color:blue" @click="go_to_agreement">《来往租车协议》</text>，并授权获取本机号码一键登录
					</view>
				</label>
			</view>
		</u-popup>

	</view>
</template>

<script>
	import {
		univerifyLogin,
		univerifyErrorHandler
	} from '../../common/univerify.js'
	export default {
		data() {
			return {
				phone: '',
				// 一键登录的变量
				show_login_one: false,
				checked_one_login: false,
				provide: [],
				hasAppleLogin:false,
				hasProvider:false
			}
		},
		methods: {
			// 点击微信登录
			wxlogin() {

			},
			// 支付宝登录
			aliopenlogin() {

			},
			// 免验证登录
			not_verification() {
				this.show_login_one = true;
			},
			// 点击下一步
			submit() {
				const that = this
				uni.setStorageSync('mobile',this.phone)
				if (!/^1\d{10}$/.test(this.phone)) {
					uni.showModal({
						content: '请输入正确的手机号',
						showCancel: false
					})
					return
				}
				uni.navigateTo({
					url: "../login_verification/login_verification",
					events: {
						translate: function(data) {
							console.log("translate", data)
						}
					},
					success: function(res) {
						res.eventChannel.emit('true', {
							phone: that.phone
						})
					}
				})
			},
			// 是否同意协议
			change_checked() {
				this.checked_one_login = !this.checked_one_login
			},
			// 删除弹窗
			delete_toast() {
				this.show_login_one = false
			},
			// 一键登录
			one_login() {
				if (this.checked_one_login) {
					univerifyLogin().catch(err => {
						if (typeof err === 'boolean') return;
						univerifyErrorHandler(err);
					})
				} else {
					uni.showToast({
						title: '请先同意协议！！',
						icon: 'error'
					})
				}
			},
			// 其他登录
			other_login() {
				this.show_login_one = false
				console.log("其他登录！！")
			},
			// 跳转协议
			go_to_agreement() {
				console.log("去看协议");
			},
			initProvider() {
				uni.getProvider({
					service: 'oauth',
					success: (res) => {
						console.log(`getProvider${res.provider}`);
						if (res.provider && res.provider.length) {
							if (res.provider.indexOf('apple') !== -1) {
								this.hasAppleLogin = true;
							}
							this.hasProvider = true;
						}
					},
					fail: (err) => {
						console.error('获取服务供应商失败：' + JSON.stringify(err));
					}
				});

			}

		},
		onLoad() {
			this.initProvider();

		}
	}
</script>

<style>
	.img {
		width: 100rpx;
		height: 100rpx;
	}

</style>
