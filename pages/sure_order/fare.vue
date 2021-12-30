<template>
	<view>
		<u-navbar back-icon-color="white" title="费用明细" title-color="white" :background="background">
			<u-icon slot="right" name="kefu-ermai" color="white" size="45" style="margin-right: 35rpx;"></u-icon>
		</u-navbar>
		<view class="top">
			<view style="margin-top:40rpx">实付</view>
			<view style="font-size: 90rpx;font-weight: bold;letter-spacing: 9rpx;">¥{{total}}</view>
			<view style="margin-top: 40rpx;">{{timer}}</view>
		</view>
		<view class="mid">
			<view class="item1">
				<view>预计消费:</view>
				<view style="flex: 1;text-align: right;">{{pre}}元</view>
			</view>
			<view class="item1">
				<view>实际消费:</view>
				<view style="flex: 1;text-align: right;">{{pre}}元</view>
			</view>
			<view style="font-size: 22rpx;color: #787878;">{{text}}</view>
			<view style="flex: 1;text-align: right;font-size: 25rpx;color: #FF5500">付费记录</view>
			<view class="item1">
				<view>基础费用:</view>
				<view style="flex: 1;text-align: right;">{{basic}}元</view>
			</view>
			<view class="item1">
				<view>押金:</view>
				<view style="flex: 1;text-align: right;">{{pre}}元</view>
			</view>
		</view>
		<view class="bottom">
			<button class="bu" @click="re">确认</button>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				background:{
					backgroundColor: '#ff5500',
				},
				total:500,
				timer:'',
				pre:509,
				basic:500,
				ya:5000,
				text:'(预计费用仅供参考，请以订单结算后实际费用为准)'
				
			}
		},
		methods:{
			onShow(){
				var date = new Date(),
				k="AM",
				year = date.getFullYear(),
				month = date.getMonth() + 1,
				day = date.getDate(),
				hour = date.getHours() < 10 ? "0" + date.getHours() : date.getHours(),
				minute = date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes();
				day >= 0 && day <= 9 ? (day = "0" + day) : "";
				if(hour>12)
				{
					hour=hour-12;
					k="PM";
				}
				this.timer = year + "年" + month + '月' + day + '号' + hour + ':' + minute+k;
			},
			re(){
				uni.navigateBack({
					url:'./sure_order'
				})
			}
			
		}
		
	}
</script>

<style>
	.top{
		background-color: #ff5500;
		height:350rpx;
		border-bottom-left-radius: 35rpx;
		border-bottom-right-radius: 35rpx;
		color:white;
		display: flex;
		flex-direction: column;
		align-items: center;
		box-shadow: 5rpx 8rpx 15rpx #c8c8c8;
		
	}
	.mid{
		display: flex;
		flex-direction: column;
		margin-top: 80rpx;
		margin-left:40rpx;
		margin-right:40rpx;
	}
	.item1{
		display: flex;
		font-size: 35rpx;
		margin-top: 30rpx;
	}
	.bu{
		/* display: flex; */
		background-color:  #ff5500;
		color:white;
		height:80rpx;
		width:40%;
		line-height: 80rpx;
		font-size:34rpx;
		border-radius: 80rpx;
		/* margin-right:0rpx; */
		
		
	}
	.bottom{
	/* display:flex;
	flex-direction: column;
	align-items: center; */
	height:90rpx;
	width:100%;
	bottom:40rpx;
	position:fixed;
	font-size:18rpx;
	}
</style>
