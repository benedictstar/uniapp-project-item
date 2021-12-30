<template>
	<view>
		<u-navbar :is-back="false" title="关于我">
			<!-- #ifdef APP-PLUS -->
				<view class="slot-wrap">
					<view class="com" @click="quit">取消</view>
				</view>
				<view slot="right" class="right" @click="complete">
					完成
				</view>
			<!-- #endif -->
			<!-- #ifndef APP-PLUS -->
				<view class="slot-wrap">
					<view class="com" @click="complete">完成</view>
				</view>
			<!-- #endif -->
		</u-navbar>
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<u-modal v-model="show" :content="content"></u-modal>
		<view style="background-color: #ffffff;
			margin-left:30rpx;margin-right:30rpx;border-radius: 16rpx;">
			<u-input :clearable="false" v-model="introduce" type="textarea" placeholder="请用一段自我介绍,展示独一无二的你~" style="margin-left: 30rpx;
			margin-right: 30rpx;font-size: 30rpx;" height="230" maxlength="200" @input="fo"
			></u-input>
			<view style="text-align:right;font-size: 20rpx;height: 50rpx;margin-right: 30rpx;color: #818181;">{{total}}/200</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				introduce:'',
				total:0,
				show:false,
				content:'关于我不能为空'
			}
		},
		methods:{
			onShow(){
				this.introduce=getApp().globalData.introduce;
				this.total=getApp().globalData.introduce.length
			},
			fo(){
				this.total=this.introduce.length
			},
			quit(){
				uni.navigateBack()
			},
			complete(){
				if(this.introduce==''||this.introduce == null || this.introduce== undefined)
				{
					this.show=true;
				}
				else{
					getApp().globalData.introduce=this.introduce;
					this.show=false;
					uni.navigateBack();
				}
				
			}
		}
	}
</script>

<style>
	page{
		background-color: #ebebeb;
	}
	.com{
		margin-left:30rpx;
		font-size: 27rpx;
		color:#ff5500;
	}
	.right{
		margin-right:30rpx;
		font-size: 27rpx;
		color:#ff5500
	}
</style>
