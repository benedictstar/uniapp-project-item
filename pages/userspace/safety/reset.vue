<template>
	<view>
		<u-navbar title=" "></u-navbar>
		<view style="font-weight: bold;margin-top:30rpx;font-size:40rpx;margin-left:25rpx">重新设置密码</view>
		<view style="margin:30rpx;">
			<u-form-item>
				<u-input :clearable="false" placeholder="" v-model="number" :disabled="true" :border="true"
				:style="[s]"></u-input>
			</u-form-item>
			<u-form-item>
				<u-toast ref="uToast"></u-toast>
				<u-verification-code :seconds="seconds" ref="uCode" 
						@change="codeChange"></u-verification-code>
				<u-input :clearable="false" placeholder="请输入验证码" v-model="check" maxlength="6" :border="true"
				style="border-radius: 40rpx;background-color: #f7f7f7"></u-input>
				<button slot="right" style="margin:20rpx;background-color:#ff5500;color: white;font-size: 23rpx;" @tap="getCode">{{tip}}</button>
			</u-form-item>
			<u-form-item>
				<u-input :clearable="false" placeholder="确认新密码" v-model="password" maxlength="16" :border="true"
				style="border-radius: 40rpx;background-color: #f7f7f7" type="password" :password-icon="false">
				</u-input>
			</u-form-item>
			<view style="font-size: 20rpx;">{{tips}}</view>
		</view>
		<view style="display: flex;flex-direction: column;align-items: center;margin-top:80rpx;margin-left: 40rpx;margin-right: 40rpx;">
			<button class="bu" @click="sure1">确认</button>
		</view>
		<u-modal v-model="show1" :content="content1"></u-modal>
		<u-modal v-model="show2" :content="content2"></u-modal>
		<u-modal v-model="show3" :content="content3"></u-modal>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				number:'',
				check:'',
				password:'',
				tips:'必须是xxx',
				s:{
					borderRadius: '40rpx',
					backgroundColor: '#f7f7f7',
				},
				show1:false,
				content1:'请输入新密码',
				show2:false,
				content2:'必须是xxx',
				show3:false,
				content3:'请输入验证码',
				tip:'',
				seconds:60
			}
		},
		methods:{
			onShow(){
				this.number=getApp().globalData.numbers
			},
			sure1(){
				if(this.password==''||this.password == null || this.password== undefined)
				{
					this.show1=true;
				}
				// 密码格式不正确
				// else if(){
					
				// }
				else if(this.check==''||this.check == null || this.check== undefined)
				{
					this.show3=true;
				}
				else{
					getApp().globalData.password=this.password
					uni.navigateBack()
				}
			},
			codeChange(text) {
							this.tip = text;
						},
			getCode() {
						if(this.$refs.uCode.canGetCode) {
								// 模拟向后端请求验证码
							uni.showLoading({
								title: '正在获取验证码'
							})
							setTimeout(() => {
								uni.hideLoading();
							// 这里此提示会被this.start()方法中的提示覆盖
								this.$u.toast('验证码已发送');
									// 通知验证码组件内部开始倒计时
								this.$refs.uCode.start();
								}, 2000);
							} else {
								this.$u.toast('倒计时结束后再发送');
							}
						},
		}
	}
	
</script>

<style>
	.bu{
		/* display: flex; */
		background-color: #ff5500;
		color:white;
		height:80rpx;
		width:100%;
		font-size:28rpx;
		border-radius: 40rpx;
		line-height:80rpx;
		/* margin-left:12%;
		margin-top:15rpx;
		margin-bottom:15rpx; */
		/* margin-right:0rpx; */
		
		
	}
</style>
