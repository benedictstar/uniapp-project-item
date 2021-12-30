<template>
	<view>
		<view class="main">
			<image :src="src" style="width:150rpx;height:150rpx;"></image>
			<view class="mid">将{{tele}}所绑定的账号注销</view>
		</view>
			<u-card style="background-color: #f7f7f7;" :head-border-bottom="false">
				<view slot="head" style="font-size:26rpx;text-align:center">注意,注销账号后以下信息将被清空且无法找回</view>
				<view slot="body" style="font-size:23rpx;">身份、账户信息、会员及权益信息</view>
				<view slot="body" style="margin-top: 30rpx;font-size:23rpx;">银行卡的快捷支付服务</view>
				<view slot="body" style="margin-top: 30rpx;font-size:23rpx;">交易记录</view>
				<view slot="foot" style="font-size:23rpx;">请确保所有交易已完结且无纠纷，账户删除后的历史交易可能产生的资金退回权益等将视作自动放弃</view>
			</u-card> 
		<view style="background-color: #f1f1f1;
			margin-left:30rpx;margin-right:30rpx;border-radius: 16rpx;">
			<u-input :clearable="false" v-model="reson" type="textarea" placeholder="请填写注销原因" style="margin-left: 30rpx;
			margin-right: 30rpx;font-size: 30rpx;" height="230" maxlength="200" @input="fo"
			></u-input>
			<view style="text-align:right;font-size: 20rpx;height: 50rpx;margin-right: 30rpx;color: #818181;">{{total}}/200</view>
		</view>
		<view style="display: flex;flex-direction: column;align-items: center;margin-top:30rpx;margin-left: 30rpx;margin-right: 30rpx;">
			<button class="bu" @click="">提交申请</button>
		</view>
		<view style="display: flex;flex-direction: column;align-items: center;font-size: 20rpx;">
			<text>点击【提交申请】即代表你已经同意</text>
			<text style="color:#FF5500;">《用户注销协议》</text>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				src:'/static/5.png',
				tele:'',
				total:0,
				reson:'',
			}
		},
		methods:{
			onShow(){
				this.tele=getApp().globalData.numbers
			},
			fo(){
				this.total=this.reson.length
			}
		}
		
	}
</script>

<style>
	.mid{
		/* margin-left:65rpx; */
		font-size:33rpx;
		margin-top:20rpx;
		font-weight: bold;
	}
	.main{
		margin-left:50rpx;
		margin-top: 20rpx;
		margin-right:50rpx;
		display: flex;
		flex-direction:column;
		align-items: center;
	}
	.bu{
		/* display: flex; */
		background-color: #ff5500;
		color:white;
		height:70rpx;
		width:100%;
		font-size:28rpx;
		border-radius: 40rpx;
		line-height:70rpx;
		/* margin-left:12%;
		margin-top:15rpx;
		margin-bottom:15rpx; */
		/* margin-right:0rpx; */
		
		
	}
</style>
