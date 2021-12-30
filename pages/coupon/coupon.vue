<template>
	<view class="coupon_page">
		
		<view class="topbackground" style="overflow: hidden;">				
			<div class="wrap">
			  <div class="inner"  @click="choose" style="margin-top: 100rpx;">{{city_choice}} ▼</div>
			</div>
		</view>					
		<view class="city_box">
			<view class="city">
				<!-- <t-city @from_son_to_father="back_to_main_page" /> -->
			</view>		
		</view>
		<!-- 头部标题 -->
		<view class="title_box">
			<view class="title">更多平台优惠不止</view>
		</view>
		<!-- 优惠券框架 -->
		<view class="coupon_box">
			<view class="coupon_item" v-for="(item, i) in list" :key="i" >
				<view class="item_info">
					<view class="coupon_list_left">
						<view class="coupon_money">{{item.reduction_amount}}</view>
						<view class="coupon_type">{{item.type}}</view>
					</view>
						
					<view class="coupon_list_right">
						<view class="coupon_list_right_top">
							<view class="top_box">
								<view class="coupon_title">{{item.title}}</view>
								<view class="coupon_time">{{item.time}}</view>
							</view>
							<view class="coupon_button_box">
								<!-- <view class="coupon_button" :class="{'coupon_button' : flag,'coupon_button2': !flag}" @click="sumit123">立即领取</view> -->
								<view class="coupon_button"@click="sumit(i)" v-bind:class="{ 'btn2' : item.flag, 'btn1': !item.flag}">{{item.con}}</view>
									 
									
								
							</view>
						</view>
						
						<view class="coupon_detail_message_box" @click="toggledetail(i)">
							<view class="coupon_detail_message">详细信息</view>
							<view class="coupon_xiala"> ▼ </view>
						</view>
					</view>
				</view>
				<view class="detailShowbox">
					<view class="item_detail" v-if="detailShowList[i]">{{item.detail}}</view>
				</view>	
				
			</view>
		</view>
		
		<button type="default" class="go_to_main" size="default" @click="go_to_main">立即租车</button>
		
	</view>
	

</template>

<script>
	export default{
		data(){
			return{
				con:"立即领取",
				detailShowList: [],
				city_choice:'',
				list: [
					{
						con:"立即领取",
						reduction_amount: 200,
						title: '盛夏满2000元减240元',
						flag: false,
						time: '2021-4-18 00;00;00 ~ 2021-7-12 00;00;00',
						type:'优惠券',
						detail: '活动期间满2000元减2500元'
					},
					{	
						con:"立即领取",
						reduction_amount: 200,
						title: '盛夏满2000元减240元',
						flag: false,
						time: '2021-4-18 00;00;00 ~ 2021-7-12 00;00;00',
						type:'优惠券',
						detail: '活动期间满2000元减2500元'
					},
					{	
						con:"立即领取",
						reduction_amount: 200,
						title: '盛夏满2000元减240元',
						flag: false,
						time: '2021-4-18 00;00;00 ~ 2021-7-12 00;00;00',
						type:'优惠券',
						detail: '活动期间满2000元减2500元你好你好你好你好你好你好你好你好你好'
					},
					{
						con:"立即领取",
						reduction_amount: 200,
						title: '盛夏满2000元减240元',
						flag: false,
						time: '2021-4-18 00;00;00 ~ 2021-7-12 00;00;00',
						type:'优惠券',
						detail: '活动期间满2000元减2500元你好你好你好你好你好你好你好你好你好'
					},
					{	
						con:"立即领取",
						reduction_amount: 200,
						title: '盛夏满2000元减240元',
						flag: false,
						time: '2021-4-18 00;00;00 ~ 2021-7-12 00;00;00',
						type:'优惠券',
						detail: '活动期间满2000元减2500元你好你好你好你好你好你好你好你好你好'
					},
					{	
						con:"立即领取",
						reduction_amount: 200,
						title: '盛夏满2000元减240元',
						flag: false,
						time: '2021-4-18 00;00;00 ~ 2021-7-12 00;00;00',
						type:'优惠券',
						detail: '活动期间满2000元减2500元你好你好你好你好你好你好你好你好你好'
					},
					{	
						con:"立即领取",
						reduction_amount: 200,
						title: '盛夏满2000元减240元',
						flag: false,
						time: '2021-4-18 00;00;00 ~ 2021-7-12 00;00;00',
						type:'优惠券',
						detail: '活动期间满2000元减2500元你好你好你好你好你好你好你好你好你好'
					},
					{
						con:"立即领取",
						reduction_amount: 200,
						title: '盛夏满2000元减240元',
						flag: false,
						time: '2021-4-18 00;00;00 ~ 2021-7-12 00;00;00',
						type:'优惠券',
						detail: '活动期间满2000元减2500元你好你好你好你好你好你好你好你好你好'
					},
				],
				
			}
			
		},
		onShow()
		{
			this.city_choice = getApp().globalData.city_choice_coupon;
		},				
		methods:{
			toggledetail(i){
				this.$set(this.detailShowList, i, !this.detailShowList[i]);
			},
			sumit(i){
			  // this.flag=!this.flag;
			  this.list[i].flag = true
			  if(this.list[i].flag==true){
			     this.list[i].con="已领取";
			  }else if(this.list[i].flag==false){
			     this.list[i].con="立即领取";
				//领取状态
			}
			},
			go_to_main()
			{
				uni.switchTab({
					url:"../mian_page/mian_page"
				})
			},
			choose()
			{
				getApp().globalData.is_from_coupon = 1;
				uni.redirectTo({
					url:'../city_choice/city_choice'
				})
			}
		
	}

	}
</script>

<style lang="scss">
	.wrap {
	  float: left; /* 自适应内容宽度 */
	  position: relative;
	  left: 50%; 
	}
	.inner {
	  position: relative;
	  left: -50%; 
	}
	page{
		background-color:#F8F8F8;
		
	}
	.topbackground{
		width: 100%;
		height: 250rpx;
		background-image: linear-gradient(to right, #fa709a ,#fee140);
	}
	.title_box{
		width: 100%;
		height: 150rpx;
		
	}
	.title{
		color: transparent;
		-webkit-text-stroke: 1px #FF5500;
		letter-spacing: 0.04em;
		text-align: center;
		line-height: 150rpx;
		font-size: 50rpx;
		
	}
	.coupon_box{
		padding-top: 50rpx;
	}
	.item_info{
		
		height: 180rpx;
		border: 1rpx solid #e4e4eb;
		border-radius: 5rpx;
		margin: 0 auto;
		display: flex;
		flex-wrap: nowrap;
		
	}
	.coupon_list_left{
	height: 100%;
	min-width: 200rpx;
	background-color: #FF5500;
	
		

		
	}
	.coupon_money{
		font-size: 80rpx;
		justify-content: center;
		text-align: center;
		color: #FFFFFF;
	}
	.coupon_type{
		font: 15rpx;
		text-align: center;
		color: #FFFFFF;
	}
	
	.coupon_list_right_top{
		display: flex;
		justify-content: space-between;	
		flex-wrap: nowrap;
		align-items: center;
		// border-bottom: 1rpx solid #333333;
		padding: 0 15rpx;
		margin-bottom: 15rpx;
		
	}
	.coupon_button_box{
		min-width: 120rpx;
		height: 36rpx;
		margin-left: 20rpx;
	}
	
	
	
	
	.coupon_title{
		font-size: 30rpx;
	}
	.coupon_time{
		font-size: smaller;
		color: #808080;
	}
	
	.coupon_list_right_bottom{
		display: flex;
		justify-content: space-between;
	}
	.coupon_detail_message_box{
		display: flex;
		justify-content: space-between;
		margin: 0 15rpx;
		border-top:1rpx solid #555555 ;
	}
	.coupon_detail_message{
		padding-top: 20rpx;
		color: #999999;
		font-size: 12rpx;
	}
	.coupon_xiala{
		padding-top: 20rpx;
		color: #999999;
		font-size: 12rpx;
	}

		
	.coupon_item {
		width: 90%;
		display: flex;
		flex-direction: column;
		margin: 0 auto;
		// background: radial-gradient(circle, #fff 2px, #fff, transparent 3px, transparent 4px, transparent 4px, sparent);

		
	}
	.detailShowbox{
	padding-bottom:30rpx;
	// display: flex;
	// flex-wrap: wrap;
		
	}
	.item_detail{
		// height: 80rpx;
		border-bottom: 1rpx solid #DCDCDC;
		border-left: 1rpx solid #DCDCDC;
		border-right:1rpx solid #DCDCDC;
		font-size: 12rpx;
		color:#999999;
		
		padding-top: 20rpx;
		padding-bottom: 20rpx;
	}
	
	// .coupon_button_box{
	// 	width: 120rpx;
	// 	height: 40rpx;
	// 	background-color: #FF5500;
	// 	border-radius: 20rpx;
	// }
	.coupon_button{
		font-size: 19rpx;
		text-align: center;
		line-height: 40rpx;
		color: #FFFFFF;
	}
	.btn1{
		background-color: #FF5500;
		border-radius: 20rpx;
		width: 90%;
		color: #FFFFFF;
		
	}
	.btn2{
		background-color: #bdbebd;
		border-radius: 20rpx;
		width: 90%;
		color: #FFFFFF;
	}
	.go_to_main
	{
		width: 80%;
		margin: 0 auto;
		margin-bottom: 20rpx;
		background-color: #FF5500;
		color: white;
	}
	
	
</style>
