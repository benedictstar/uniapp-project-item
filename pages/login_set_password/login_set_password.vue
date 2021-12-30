<template>
	<view>
		<view class="" style="font-size: 60rpx; font-weight: 700; width: 90%; margin: 0 auto;">
			设置登录密码
		</view>
		<view class=""style="font-size: 10rpx; color: #999; width: 90%; margin: 0 auto;">
			您可以使用设置的新密码在来往出行app登录您的账号
		</view>
		<view class="" style="margin-top: 100rpx;">
			
			<input type="password" value="" style="border-bottom: 1rpx #999 solid; width: 90%; margin: 0 auto; height: 100rpx;" placeholder="8-16位密码" />			
			<view class="" style="font-size: 10rpx; color: #999; width: 90%; margin: 0 auto;">
				需包含数字、字母、符号中至少2种元素，密码长度需8-16位
			</view>	
		</view>
		<view class="" style="width:100%;">
			<view class="" @click="submit" style="font-size: 30rpx; width: 80%; margin: 0 auto;height: 80rpx;text-align: center; line-height: 80rpx; background-color: orange; color: white; margin-top: 50rpx;">
				确认
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			submit()
			{
				
			}
			
		}
	}
</script>

<style>

</style>
