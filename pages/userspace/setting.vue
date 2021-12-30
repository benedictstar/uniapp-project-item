<template>
	<view>
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<u-cell-group>
			<u-cell-item title="个人信息" value="去完善" @click="personal"></u-cell-item>
			<u-cell-item title="账号安全" @click="security"></u-cell-item>
			<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<u-cell-item title="紧急联系人" value="初次设置可得500来往币" @click="urgent"></u-cell-item>
			<u-cell-item title="常用驾驶人" value="去添加" @click="usual"></u-cell-item>
			<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<u-cell-item title="消息推送设置" value="" @click="infsetting"></u-cell-item>
			<u-cell-item title="隐私" value="" @click="privacy"></u-cell-item>
			<u-cell-item title="关于我们" value="" @click="we"></u-cell-item>
		</u-cell-group>
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<view style="height: 100rpx; width:100%;background-color: #FFFFFF;
		text-align: center; line-height: 110rpx;font-size: 30rpx;color:#ff5500" @click="out">退出登录</view>
	</view>
</template>

<script>
	export default{
		methods:{
			personal(){
				uni.navigateTo({
					url:'person/personal'
				})
			},
			security(){
				uni.navigateTo({
					url:'safety/safety'
				})
			},
			urgent(){
				uni.navigateTo({
					url:'urgent/urgent'
				})
			},
			usual(){
				uni.navigateTo({
					url:'usual/usual'
				})
			},
			infsetting(){
				uni.navigateTo({
					url:'inf/infsetting'
				})
			},
			privacy(){
				uni.navigateTo({
					url:'privacy/privacy'
				})
			},
			we(){
				uni.navigateTo({
					url:'we/we'
				})
			},
			out(){
				
			}
		}
	}
</script>

<style>
	page{
		background-color: #ebebeb;
	}
</style>
