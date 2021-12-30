<template>
	<view style="background-color: rgb(255, 255, 204); color: black;overflow :hidden">
		<!-- 顶部说明栏 -->
		<view class="" style="width: 90%;margin: 0 auto; margin-top: 20rpx; margin-bottom: 30rpx;">
			<view class="" style="font-size: 30rpx; font-weight: 600;">
				对长租有疑问？
			</view>
			<view class="">
				<text>
					通过首页右上方的客服通道与客服联系，我们将为您提供最优质的服务已最优惠的价格。
					(长租30天起呦)
				</text> 
			</view>		
		</view>
		
		<!-- 选择长租的方式 -->
		<view class="" style="display: flex; width: 90%; margin: 0 auto;">
			<view class="rent_style" @click="change_to_person" :class="{'choosing':!is_company,'not_choosing':is_company}">
				个人长租
			</view>
			<view class="rent_style" @click="change_to_company" :class="{'choosing':is_company,'not_choosing':!is_company}">
				企业长租
			</view>
		</view>
		
		<!-- 长租内容 -->
		<view class="" style="margin-top: 30rpx;">
			<view class="" style="font-size: 30rpx; width: 100%; text-align: center;">
				联系方式
			</view>			
			<view class="each_input" v-if="is_company"><label class="label_style">公司</label><input  type="text" v-model="formData.company" placeholder="请输入公司全名" placeholder-class=" placeholder_style"></view>
			  
			<view class="each_input"><label class="label_style">联系人姓名</label><input  type="text" v-model="formData.name_person" placeholder="请输入联系人姓名" placeholder-class=" placeholder_style"></view>
			  
			<view class="each_input"><label class="label_style">联系人手机号</label><input type="phone" v-model="formData.phone" placeholder="请输入11位手机号" placeholder-class=" placeholder_style"></view>

			 <view class="each_input" style="display: flex; justify-content: space-between;">
			  	<label class="label_style">其他要求</label> <textarea :value="formData.need" placeholder="如果有其他要求请备注说明"placeholder-class=" placeholder_style_need" id="other_need" style="height: 300rpx; width: 400rpx;border: 1rpx solid #999;" />			  	
			 </view>
			 
		     <view class="" style="font-size: 30rpx; width: 100%; text-align: center;margin-top: 30rpx;">
				租车详情
			</view>
			<view class="each_input"><label class="label_style">租车城市</label><input  type="text" v-model="formData.city" placeholder="请选择租车城市" placeholder-class=" placeholder_style"></view>
			  
			<view class="each_input"><label class="label_style">租车日期</label><input  type="text" v-model="formData.date" placeholder="请输入租车日期" placeholder-class=" placeholder_style"></view>
			  
			<view class="each_input"><label class="label_style">租车类型</label><input type="phone" v-model="formData.car_type" placeholder="请选择租车类型" placeholder-class=" placeholder_style"></view>
    	</view>
		
		<view class="" @click="submit" style="border-radius: 15rpx; line-height: 70rpx; text-align: center; height: 70rpx; width: 90%; margin: 0 auto;  margin-top: 40rpx;  margin-bottom: 40rpx; color: white; background-color: orange;">
			提交
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				is_company:0,
				formData:{
					company:'',
					name_person:'',
					phone:'',
					need:'',
					city:'',
					date:'',
					car_type:''
				}
			}
		},
		methods: {
			// 变成公司长租样式
			change_to_company(){
				this.is_company = 1;
			},
			// 变成个人长租样式
			change_to_person()
			{
				this.is_company = 0;
			},
			submit()
			{
				console.log("submit!!");
				uni.switchTab({
					url:"../mian_page/mian_page"
				})
			}
		},
		onLoad()
		{			
		}
	}
</script>

<style>
	.choosing{
		background-color:  rgb(255, 102, 0);
	}
	.not_choosing{
		background-color:rgb(255, 204, 153);
		color: #000000;
	}
	.placeholder_style{
		font-size: 10rpx;
		margin-left: 10rpx;
	}
	.placeholder_style_need
	{
		font-size: 10rpx;
		position: relative;
		left: 10rpx;
	}
	.each_input{
		display: flex;
		justify-content: space-between;
		width: 90%;
		margin: 0 auto;
		margin-top: 30rpx;
	}
	.each_input input{
		border: 1rpx solid #999;
		width: 400rpx;
	}
	.rent_style{
		width: 50%;
		height: 80rpx;
		line-height: 80rpx;
		text-align: center;
		font-size: 35rpx;
		
	}
</style>
