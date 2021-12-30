<template>
	<view>
		<!-- <u-navbar title="服务条款"></u-navbar> -->
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<u-cell-group>
			<u-cell-item title="平台规则" value="" @click="rule"></u-cell-item>
			<u-cell-item title="服务条款" value=""  @click="it"></u-cell-item>
			<u-cell-item title="保障条款" value="" @click="security"></u-cell-item>
			<u-cell-item title="保障细则" value="" @click="detail"></u-cell-item>
		</u-cell-group>
		<!-- <u-popup mode="bottom" height="1280" :closeable="true" v-model="show1" close-icon-pos="top-left" :mask="false">
			<view style="font-weight: bold;margin-top:100rpx;font-size:40rpx;margin-left:25rpx;">《来往出行服务规则》</view>
		</u-popup>
		<u-popup mode="bottom" height="1280" :closeable="true" v-model="show2" close-icon-pos="top-left" :mask="false">
			<view style="font-weight: bold;margin-top:100rpx;font-size:40rpx;margin-left:25rpx;position: fixed;">服务条款</view>
		</u-popup>
		<u-popup mode="bottom" height="1280" :closeable="true" v-model="show3" close-icon-pos="top-left" :mask="false">
			<view style="font-weight: bold;margin-top:100rpx;font-size:40rpx;margin-left:25rpx;position: fixed;">保障服务规则</view>
		</u-popup>
		<u-popup mode="bottom" height="1280" :closeable="true" v-model="show4" close-icon-pos="top-left" :mask="false">
			<view style="font-weight: bold;margin-top:100rpx;font-size:40rpx;margin-left:25rpx;position: fixed;">保障细则</view>
		</u-popup> -->
	</view>
</template>

<script>
	export default{
		data(){
			return{
				// show1:false,
				// show2:false,
				// show3:false,
				// show4:false,
			}
		},
		methods:{
			rule(){
				uni.navigateTo({
					url:'./rules'
				})
			},
			it(){
				uni.navigateTo({
					url:'./it'
				})
			},
			security(){
				uni.navigateTo({
					url:'./security'
				})
			},
			detail(){
				uni.navigateTo({
					url:'./detail'
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
