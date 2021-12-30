<template>
	<view>
		<view class="" style="font-size: 60rpx; font-weight: 700; width: 90%; margin: 0 auto;">
			请您输入验证码
		</view>
		<view class=""style="font-size: 10rpx; color: #999; width: 90%; margin: 0 auto;">
			验证码已经发送到您的手机
		</view>
		<view class="" style="margin-top: 100rpx;">
			<view class="" style="font-size: 10rpx; color: #999; width: 90%; margin: 0 auto;">
				6位数字验证码
			</view>		
			 <one-input ref="password" @finish="loginBySms" type="box" style="margin-top: 10rpx; margin-bottom: 10rpx;"></one-input>			
			<view class="" style="font-size: 10rpx; color: #999; width: 90%; margin: 0 auto;display: flex; ">
				没收到验证码？
				 <view class='can_choose' v-if="if_over_time" @click="sendSmsCode">
				 	重新发送验证码	
				 </view>
				 <view class='not_choose' v-if="!if_over_time" >
				 	重新发送验证码<text class="">({{seconds}}s)后</text>	
				 </view>
			</view>	
		</view>
	</view>
</template>

<script>
	import oneInput from '@/components/myp-one/myp-one.vue'

	export default {
		data() {
			return {
				phone:"",
				seconds: 0,
				if_over_time: 0,
				
			}
		},
		components: {
			oneInput
		},
		onShow() {
			this.seconds = 60;
			let that = this;
			that.if_over_time = 0;
			let reciprocal = setInterval(function() {
				that.seconds--;
				if (that.seconds == 0) {
					clearInterval(reciprocal);
					that.if_over_time = 1;
				}
			}, 1000)
		},
		methods: {
			sendSmsCode(type) {
				uniCloud.callFunction({
					name: 'uni-id-test',
					data: {
						action: 'sendSmsCode',
						params: {
							mobile: this.phone,
							type
						},
						success(res) {
							uni.showModal({
								showCancel: false,
								content: JSON.stringify(res.result)
							})
						},
						fail(e) {
							console.error(e)
							uni.showModal({
								showCancel: false,
								content: '发送失败，请稍后再试'
							})
						}
					}
				})
			},
			// 输入完成后调用
			loginBySms(mycode) {
				console.log(mycode)
				uniCloud.callFunction({
					name: 'uni-id-test',
					data: {
						action: 'loginBySms',
						params: {
							mobile: this.mobile,
							code: mycode
						}
					},
					success: (res)=>{
						uni.showModal({
							showCancel: false,
							content: JSON.stringify(res.result)
						})
						if (res.result.code === 0) {
							uni.setStorageSync('uni_id_token', res.result.token)
							uni.setStorageSync('uni_id_token_expired', res.result.tokenExpired)
						}
						uniCloud.callFunction({
							name:"user-center",
							data:{
								action:"login",
								mobile:this.phone
							}
						}).then(res=>{
							uni.setStorageSync('nickname',res.result.data[0].nickname)
							uni.setStorageSync('avatar',res.result.data[0].avatar)
							uni.setStorageSync('sex',res.result.data[0].sex)
							uni.setStorageSync('birthday',res.result.data[0].birthday)
						})
					},
					fail(e) {
						console.error(e)
						uni.showModal({
							showCancel: false,
							content: '登录失败，请稍后再试'
						})
					}
				})
			},
			send_verificaition() {
				sendSmsCode('login')
				console.log("发送验证码！");
				this.seconds = 60;
				let that = this;
				that.if_over_time = 0;
				let reciprocal = setInterval(function() {
					that.seconds--;
					if (that.seconds == 0) {
						clearInterval(reciprocal);
						that.if_over_time = 1;
					}
				}, 1000)
			}
		},
		onLoad() {
			const that = this
			//接受login_main页面传参
			const eventChannel = this.getOpenerEventChannel()
			eventChannel.emit('translate', {
				data: 'test'
			});
			eventChannel.on('true', function(data) {
				that.phone = data.phone
				sendSmsCode('login')
			})
		}
	}
</script>

<style>
	.can_choose {
		color: blue;
	}

	.not_choose {
		color: #999;
	}
</style>
