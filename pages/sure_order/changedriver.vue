<template>
	<view>
		<view class="" style="border-bottom-left-radius:30rpx; border-bottom-right-radius:30rpx; width:100%; background-color: #E35C31; height: 200rpx;">
			
		</view>
		<view style="position: relative; top:-180rpx; background-color:white;border-radius: 30rpx; width: 90%; margin: 0 auto; margin-bottom: 30rpx;height:60rpx; line-height: 60rpx;">
			<u-icon name="plus-circle" label="新增驾驶员" 
			style="margin-left:35%;margin-top:10rpx;margin-bottom:10rpx;font-weight: bold;" size="35" 
			label-size="30" color=" #E35C31" label-color="#E35C31" @click="newd"></u-icon>
		</view>
		<!-- <view style="background-color: white;width:100%;">
			<u-radio-group style="display:flex;flex-direction: column;width:100%">
				<u-radio v-for="(item,index) in driverinf" :key="index">
					<view style="width: 200%;background-color: #007AFF;">
						<view style="font-weight: bold;font-size:25rpx;">
							{{item.name}}
						</view>
						<view>
							<text>身份证</text>
							<text style="margin-left: 40%;">{{item.idcard}}</text>
						</view>
						<view>
							<text>电话</text>
							<text style="margin-left: 40%;">{{item.tele}}</text>
						</view>
					</view>
				</u-radio>
			</u-radio-group>
		</view> -->
		<view class="common-card"style="position: relative; top:-180rpx;">
			<view class="title">已有驾驶员信息</view>
			<view class="m-content">
				<u-radio-group v-model="driveridcard" style="background-color: white;">
					<u-radio v-for="(item,index) in driverinf" :key="index" @change="change_message(index)" :name="item.idcard" :disabled="item.disabled" active-color="#ff5500" style="background-color: white;">
						<view class="" style="margin-left: 20rpx; margin-top: 10rpx; width: 500rpx;  ">
							<view class="box-head" style="font-weight: 800;">{{item.name}}</view>
							<view class="" style="font-size: smaller;">
								<view style="display: flex; justify-content: space-between;">
									<view style="flex-basis: 30%;">{{item.cardname}}</view>
									<view>{{item.idcard}}</view>
								</view>
								<view style="display: flex; justify-content: space-between;">
									<view style="flex-basis: 30%;">电话</view>
									<view>{{item.tele}}</view>
								</view>
							</view>
						</view>
					</u-radio>
				</u-radio-group>
			</view>
		</view>
		
		<view class="bottom">
			<button class="bu" @click="back">提交</button>
		</view>
	</view>
</template>

<script>
	import bottom4 from '../../components/bottom4.vue'
	export default{
		data(){
			return{
				driverinf:[],
				driveridcard:'',
			}
		},
		methods:{
			newd(){
				uni.navigateTo({
					url:'./newdriver'
				})
			},
			onLoad(){
				this.driverinf=getApp().globalData.driverinf;
				this.driveridcard=getApp().globalData.driverinf[0].idcard
			},
			back(){
				for(var i=0;i<getApp().globalData.driverinf.length;i++)
				{
					if(getApp().globalData.driverinf[i].idcard==this.driveridcard)
					{
						var m;
						m=getApp().globalData.driverinf[0];
						getApp().globalData.driverinf[0]=getApp().globalData.driverinf[i];
						getApp().globalData.driverinf[i]=m;
					}
				}
				uni.redirectTo({
					url:'./sure_order'
				})
			},
			change_message(index)
			{
				getApp().globalData.driverinf_index = 0;
				// console.log(getApp().globalData.driverinf_index)
			}
		
		},
		components: {
			bottom4,
			},
	}
</script>

<style>
	page{
		background-color: #ebebeb;
	}
	.common-card {
			background-color: #fff;
			padding: 20rpx;
			margin: 20rpx;
			border-radius: 20rpx;
			min-height:580rpx
			
		}
	.common-card .title{
			font-size: 27rpx;
			font-weight: bolder;
			margin-top: 2rpx;
		}
	.common-card .m-content{
		/* display:flex;
		flex-direction: column; */
		background-color: #fff;
	}
	.common-card .m-content .box{
		height: 10%;
		width:200%;
		/* width:95%; */
		/* background-color: #eeeeee; */
		/* margin:20rpx; */
	}
	.common-card .m-content .box .box-head{
		font-size:26rpx;
		margin:20rpx;
	}
	.common-card .m-content .box .box-content{
		font-size:20rpx;
		margin:20rpx;
		color:#585858;
		width:600rpx;
		
	}
	.bottom{
	/* display:flex; */
	height:90rpx;
	width:120%;
	bottom:0rpx;
	position:fixed;
	font-size:18rpx;
	}
	.bu{
		/* display: flex; */
		background-color:  #E35C31;
		color:white;
		height:64rpx;
		width:60%;
		text-align: center;
		font-size:28rpx;
		border-radius: 80rpx;
		margin-left:12%;
		margin-top:15rpx;
		margin-bottom:15rpx;
		/* margin-right:0rpx; */
		
		
	}
</style>
