<template>
	<view>
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<u-cell-group>
			<u-cell-item title="版本信息" value="1.0.0" @click=""></u-cell-item>
			<u-cell-item title="联系我们" :value="tele"  @click=""></u-cell-item>
			<u-cell-item title="服务条款" value="" @click="serve"></u-cell-item>
			<u-cell-item title="来往租车安全认证" value="" @click="ima"></u-cell-item>
			<u-cell-item title="举报中心" value="" @click="inform"></u-cell-item>
		</u-cell-group>
		<view class="mid">
			<image :src="qr" style="width:100rpx;height:100rpx"></image>
			<view style="margin-top: 30rpx;">{{text1}}</view>
			<view>{{text2}}</view>
		</view>
		<view class="bottom">
				<view style="display: flex;flex-direction: column;align-items: center;">来往租车 版权所有</view>
				<view style="display: flex;flex-direction: column;align-items: center;">Copyright 2020-2021</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				tele:12345,
				qr:'/static/driver.png',
				text1:'关注“来往租车”公众号 享优惠大礼',
				text2:'长按二维码即可保存'
			}
		},
		methods:{
			serve(){
				uni.navigateTo({
					url:'./item'
				})
			},
			ima(){
				uni.navigateTo({
					url:'./ima'
				})
			},
			inform(){
				uni.navigateTo({
					url:'./inform'
				})
			}
		}
	}
</script>

<style>
	page{
		background-color: #ebebeb;
	}
	.mid{
		margin-top: 80rpx;
		align-items: center;
		display: flex;
		flex-direction: column;
		font-size: 23rpx;
	}
	.bottom{
		bottom:30rpx;
		position: fixed;
		width:100%;
		/* text-align: center; */
		/* display: flex;
		flex-direction: column; */
		color:#848484;
		font-size:23rpx
	}
</style>
