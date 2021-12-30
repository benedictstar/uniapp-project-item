<!-- 消息推送页 -->
<template>
	<view>
		<u-cell-group>
			<u-cell-item title="聊天消息推送" :arrow="false" active-color="#ff5500" >
				<u-switch v-model="checked" size="30"></u-switch>
			</u-cell-item>
		</u-cell-group>
		<view class="tip">{{wen}}</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				// 用于识别开关是否打开
				checked:false,
				wen:'关闭后，其他用户与您的聊天信息仍能够收到，只是不会主动通知您'
			}
		}
	}
</script>

<style>
	page{
		background-color: #ebebeb;
	}
	.tip{
		/* margin-left:30rpx;
		margin-right:30rpx; */
		margin:30rpx;
		color:#848484;
		font-size:28rpx
	}
</style>
