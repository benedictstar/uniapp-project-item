<template>
	<view>
		<u-navbar :is-back="false" title="设置昵称">
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
		<u-modal v-model="show" :content="content"></u-modal>
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<view style="background-color: white;height:100rpx">
			<view style="margin-left:30rpx;margin-right:30rpx">
				<u-form-item><u-input height="60" placeholder="请输入昵称" v-model="nickname"/></u-form-item>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				show:false,
				content:'昵称不能为空',
				nickname:null

			}
		},
		methods:{
			onShow(){
				this.nickname=uni.getStorageSync('nickname');
			},
			quit(){
				uni.navigateBack()
			},
			complete(){
				if(this.nickname==''||this.nickname == null || this.nickname== undefined)
				{
					this.show=true;
				}
				else{
					uni.setStorageSync('nickname',this.nickname);
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
	.slot-wrap{
		
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
