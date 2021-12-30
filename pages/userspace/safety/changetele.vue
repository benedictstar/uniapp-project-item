<template>
	<view>
		<u-navbar title="换绑手机"></u-navbar>
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<view class="main">
			<view style="font-size:25rpx">您当前的手机号是</view>
			<view style="font-size:40rpx;margin-top:30rpx">{{number}}</view>
		</view>
		<view style="margin-top:70rpx;margin-left:40rpx;margin-right:40rpx">
			<view style="font-weight: bold;font-size:30rpx">友情提示:</view>
			<view style="margin-top: 30rpx;font-size:25rpx">{{text1}}</view>
			<view style="margin-top: 30rpx;font-size:25rpx">{{text2}}</view>
			<view style="margin-top: 30rpx;font-size:25rpx">{{text3}}</view>
			<view style="display: flex;flex-direction: column;align-items: center;margin-top:80rpx;">
				<button class="bu" @click="update">更换手机号</button>
			</view>
		</view>
		<u-popup mode="bottom" height="1280" :closeable="true" v-model="show" close-icon-pos="top-left" :mask="false">
			<view style="font-weight: bold;margin-top:100rpx;font-size:40rpx;margin-left:25rpx">验证当前手机号</view>
			<view style="margin:40rpx">
				<u-form ref="uForm" :model="form">
					<u-form-item label="手机号"><u-input :clearable="false" placeholder="请输入手机号码" v-model="form.number1" maxlength="11"></u-input></u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
					<u-form-item label="验证码">
						<u-toast ref="uToast"></u-toast>
						<u-verification-code :seconds="seconds" ref="uCode" 
								@change="codeChange"></u-verification-code>
						<u-input :clearable="false" placeholder="请输入验证码" v-model="form.check" maxlength="6"/>
						<button slot="right" style="margin:20rpx;background-color:#ff5500;color: white;font-size: 23rpx;" @tap="getCode">{{tip}}</button>
					</u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
				</u-form>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;margin-top:80rpx;margin-left: 40rpx;margin-right: 40rpx;">
				<button class="bu" @click="sure">确认</button>
			</view>
		</u-popup>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				number:'',
				text1:'1、换班',
				text2:'2、dd',
				text3:'3、',
				show:false,
				form:{
					number1:'',
					check:'',
				},
				tip:'',
				seconds:60,
				
			}
		},
		methods:{
			onShow(){
				// this.number='12345'
				var k;
				k=getApp().globalData.numbers;
				for(var i=0;i<k.length;i++)
				{
					this.number+=k[i];
					if(i==2||i==6){
						this.number+=' ';
					}
				}
				this.form.number1=getApp().globalData.numbers;
			},
			update(){
				this.show=true;
				
			},
			sure(){
				// 如果验证码匹配
				this.show=false;
				getApp().globalData.numbers=this.form.number1;
				this.number=this.number1;
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
						}
		}
	}
</script>

<style>
	.main{
		margin-top:100rpx;
		display:flex;
		flex-direction: column;
		align-items: center;
	}
	.bu{
		/* display: flex; */
		background-color: #ff5500;
		color:white;
		height:80rpx;
		width:100%;
		font-size:28rpx;
		border-radius: 0rpx;
		line-height:80rpx;
		/* margin-left:12%;
		margin-top:15rpx;
		margin-bottom:15rpx; */
		/* margin-right:0rpx; */
		
		
	}
</style>
