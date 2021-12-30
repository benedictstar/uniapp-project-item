<template>
	<view style="background: #ff7167;">
		<image mode="widthFix" style="width: 100%;" src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fhbimg.b0.upaiyun.com%2F0d411196eb9d7054fba06279e0dce75a3d97648715a41-lOsYjn_fw658&refer=http%3A%2F%2Fhbimg.b0.upaiyun.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1628742528&t=a21267bbc1275470abba37d4cd72a3a8">
		<!-- 活动规则 -->
		<button class="rulesBtn" size="mini" @click="togglePopup">活动规则</button>
		<uni-popup type="center" ref="popup">
			<view class="popupBox">
				<h3 style="text-align: center;margin: 20rpx;">活动规则</h3>
				<text>12345678945645631321513513123148631654651</text>
			</view>
		</uni-popup>
		
		<view>
			<!-- 去邀请好友 -->
			<view class="inviteMain">
				<!-- 收益显示 -->
				<view style="text-align: center;margin: 20rpx;">
					<view class="earningBox">
						<h4>&yen;</h4><h1>123</h1>
						<p>优惠券收益</p>
					</view>
					<view class="earningBox">
						<h4>&yen;</h4><h1>456</h1>
						<p>现金收益</p>
					</view>
				</view>
				<button class="gotoInviteBtn">去邀请好友</button>
				<!-- 奖励信息 -->
				<view style="text-align: center;margin: 20rpx; display: flex; justify-content: space-between;">
					<view class="rewardBox">
						<p>每邀请1人注册下首单得</p>
						<h4>&yen;</h4><h1>249</h1>
						<p>无门槛券</p>
					</view>
					<view class="rewardBox">
						<p>好友成为车主且完成首单</p>
						<h4>&yen;</h4><h1>188</h1>
						<p>现金奖励</p>
					</view>
				</view>
			</view>
			<!-- 操作流程图 -->
			<view class="flowchart">
				<h3>简单几步 立享奖励</h3>
				<image mode="widthFix" style="width: 75%;" src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic.baike.soso.com%2Fp%2F20131204%2Fbki-20131204111936-1353177918.jpg&refer=http%3A%2F%2Fpic.baike.soso.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1628750054&t=76bad0f7a60116deac8413f8458f7ae2"></image>
			</view>
			<view class="" style="width:100%; height: 10rpx;">
				
			</view>
		</view>
	</view>
</template>

<script>
	// import uniPopup from '../../components/uni-popup/uni-popup.vue'
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			togglePopup(){
				this.$refs.popup.open('center')
			}
		}
	}
</script>

<style>
	.rulesBtn{
		position: absolute;
		right: 0;
		top: 80rpx;
		background-color: rgba(0,0,0,0.75);
		color: #FFFFFF;
		border-radius: 0;
		border-top-left-radius: 25rpx;
		border-bottom-left-radius: 25rpx;
	}
	.popupBox{
		width: 600rpx;
		background-color: #FFFFFF;
		border-radius: 30rpx;
		padding: 30rpx;
		word-break: break-all;
	}
	.inviteMain, .flowchart{
		background-color: #FFFFFF;
		border-radius: 30rpx;
		margin: 30rpx;
		padding: 5rpx;
		text-align: center;
	}

	.earningBox{
		display: inline-block;
		padding: 10rpx;
		margin-left: 10%;
		margin-right: 10%;
	}
	.earningBox h1,h4{
		display: inline;
	}
	.earningBox p{
		font-size: 14rpx;
	}
	
	.gotoInviteBtn{
		background-color: #ffd502;
		font-weight: bold;
		margin-left: 50rpx;
		margin-right: 50rpx;
		border-radius: 50rpx;
	}
	
	.rewardBox{
		/* display: inline-block; */
		width: 48%;		
		padding: 20rpx;
		
		margin: 10rpx;
		border-radius: 30rpx;
		background-color: #ffebeb;
	}
	.rewardBox h1{
		display: inline;
		color: #ff7167;
	}
	.rewardBox h4{
		color: #ff7167;
	}
	.rewardBox p{
		font-size: smaller;	
	}
	.flowchart h3{
		padding: 20rpx;
		color: #ff7167;
	}
</style>
