<template>
	<view>
		<!-- <u-navbar title="隐私"></u-navbar> -->
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<u-cell-group>
			<u-cell-item title="隐私设置" value="" @click="root"></u-cell-item>
			<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<u-cell-item title="隐私政策" value="" @click="policy"></u-cell-item>
		</u-cell-group>
		<!-- <u-popup mode="bottom" height="1280" :closeable="true" v-model="show" close-icon-pos="top-left" :mask="false">
			<view style="font-weight: bold;margin-top:100rpx;font-size:40rpx;margin-left:25rpx;position: fixed;">来往租车隐私政策</view>
		</u-popup> -->
	</view>
	
</template>

<script>
	export default{
		data(){
			return{
				// show:false
			}
		},
		methods:{
			root(){
				uni.navigateTo({
					url:'./root'
				})
			},
			policy(){
				uni.navigateTo({
					url:'./policy'
				})
			}
			
		}
	}
</script>

<style>
	page{
		background-color: #ebebeb;
	}
</style>
