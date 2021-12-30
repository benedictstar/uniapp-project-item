<template>
	<view>
		<view class="nav">
			<u-navbar title="给车主补钱" title-color="#000" :title-bold="true">
				<u-icon slot="right" name="kefu-ermai" size="45" style="margin-right: 40rpx;"></u-icon>
			</u-navbar>
		</view>
		<view class="top">
			<u-gap height="60" bg-color="#FFF"></u-gap>
			<view style="font-size: 33rpx;margin-left: 45rpx;">补钱金额（元）</view>
			<view style="font-size: 33rpx;"><u-input inputAlign="center" height="100" :customStyle="cStyle" :clearable="false" style="font-size: 33rpx;margin-top: 10rpx;" placeholder="请输入补钱金额" type="number" v-model="form.amount" /></view>
			<view style="display: flex;flex-direction: column;align-items: center;">{{timer}}</view>
		</view>
		<view class="content" style="background-color:#f5f2f5;margin-top: 20rpx;">
			<u-form style="font-weight:600">
				<view style="margin-left: 30rpx;font-size: 30rpx;">补钱原因</view>
				<u-form-item>
					<u-radio-group v-model="value" :wrap="true" active-color="#ff5500">
						<u-radio class="u-border-bottom u-p-20 " name="1" label-size="25" style="height:60rpx">提前还车</u-radio>
						<u-radio class="u-border-bottom u-p-20" name="2" label-size="25" style="height:60rpx">油费补价</u-radio>
						<u-radio class="u-border-bottom u-p-20" name="3" label-size="25" style="height:60rpx">超里程费用</u-radio>
						<u-radio class="u-border-bottom u-p-20" name="4" label-size="25" style="height:60rpx">车损补钱</u-radio>
						<u-radio class="u-border-bottom u-p-20" name="5" label-size="25" style="height:60rpx">违章违约金</u-radio>
						<view class="u-flex">
							<u-radio class="u-border-bottom u-m-20" name="6" checked="true" label-size="25" style="height:40rpx">
								<view class="u-flex" >其他<u-input @click="otherChecked" class="u-m-l-30" placeholder="若非以上原因,请再次填写" v-model="form.reason" /></view>	
							</u-radio>
						</view>
					</u-radio-group>
				</u-form-item>
				<!-- <u-form-item class="u-p-26" label="补钱金额(元)" label-width="200" style="background-color:#fff">
					<u-input placeholder="请输入补钱金额" type="number" v-model="form.amount" />
				</u-form-item> -->
				<view class="u-p-26" style="background-color:#e5e3e5;margin-left: 20rpx;margin-right: 20rpx;
				margin-bottom: 40rpx;border-radius: 20rpx;font-size: 24rpx;">
					<text>补钱规则\n</text>
					<text>
						1.订单开始至还车后的12小时内，均可进行补钱操作，补钱金额（部分或全部）将从租车押金中扣除，具体以实际扣除金额为准，补钱的金额以最后一次操作的为准。\n
					</text>
					<text>2.如交接车时您已正确填写油表，公里数，油费和超里程费用将从租车押金中直接扣除，请在费用明细中查看。</text>
				</view>
			</u-form>
			<button class="bot" @click="submit" shape="circle">提交</button>
			
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			value:"1",
			form: {
				reason: '',
				amount: ''
			},
			cStyle:{
				
				// backgroundColor:'black',
				fontSize:'70rpx',
				fontWeight:'bold',
				letterSpacing:'5rpx'
			},
			timer:{
				
			}
			// u-radio-group的v-model绑定的值如果设置为某个radio的name，就会被默认选中
		};
	},
	methods: {
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
		otherChecked(){
			this.value="6";
		},
		submit(){
			
		}
		
	}
};
</script>

<style>
	page{
		background-color:#f5f2f5;
	}
	.top{
		height: 300rpx;
		border-bottom-right-radius: 100rpx;
		background-color:#ffffff;
		box-shadow: 5rpx 8rpx 15rpx #c8c8c8;
	}
	.bot{
		width:70%;
		height:70rpx;
		margin-bottom: 60rpx;
		color: white;
		background-color: #FF5500;
		border-radius: 35rpx;
	}
</style>
