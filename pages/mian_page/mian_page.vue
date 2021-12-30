<template>
	<view>
		<u-popup v-model="show_toast" mode="center"   :mask-close-able="false">
			<view class="" @click="delete_toast" style="position: absolute; right: 15rpx; z-index: 999;">
				X
			</view>
			<view style="width: 700rpx;height:700rpx; margin: 0 auto; ">
				
				<image src="../../static/lingquanzhongxin.png" mode="" style="width: 100%; height: 700rpx;" @click="not_show_toast"></image>
			
			</view>
		</u-popup>
		
		<!-- 协议弹出框 -->
		<u-popup v-model="show_toast_agreement" :mask-close-able="false" mode="center">
					<view class="title-box">
						<view class="title">用户协议与隐私政策</view>
					</view>
					<view class="content-box" style="width: 700rpx;height:700rpx; margin: 0 auto; " >
					<view class="content" v-for="(item,index) in contentlist" :key = "index">
					{{item}}
					</view>
					</view>
					<view class="button-box">
						<button class="dissagree" type="mini" @click="exit_agreement">不同意</button>
						<button class="agree" type="mini" @click="go_to_main">同意</button>
					</view>
				</u-popup>
		<!-- 弹窗 -->
		
		<!-- 无缝滑屏 field mode -->
		<uni-swiper-dot class="swiper_top" :info="info" :current="current" field="content" :mode="mode" :dotsStyles="dotsStyles">
		    <swiper class="swiper-box" @change="swiper_change" autoplay="true" interval=10000 >
		        <swiper-item v-for="(item ,index) in info" :key="index">
		            <view class="swiper-item">
		                <navigator url=""><image id="swiper_id" :style="swiper_style" :src="item.url" mode="aspectFit"></image></navigator>
		            </view>
		        </swiper-item>
		    </swiper>
		</uni-swiper-dot>
		
		<!-- 时间选择部分 -->
		<view class="time_choose" >
			<view class="" style="width: 94%; margin: 0 auto; margin-top: 5rpx;">
				<!-- 时间选择部分的第一行 -->
				<view class="time_choose_col" style="width: 100%; display: flex; justify-content: space-between;">
					<view class="time_choose_first" style="width: 30%;" @click="to_city_choice">
						<view class="" style="color:#999; font-size: 3rpx; width: 100%;">
							取车城市
						</view>
						<view class=""style="font-weight: 700; font-size: 40rpx; width: 100%;">
							{{city_choice}}
						</view>
					</view >
					<view class="" style="display: flex; margin-top: 30rpx; ">												
						<selectSwitch @change="changeSwitch" :switchList="switchList" :checked_bj_color="checked_bj_color" style="margin-right: 20rpx;" />
						<view class="" style="font-size: 30rpx; margin-top: 10rpx;">异地还车</view>
					</view>
				</view>
				<!-- 时间选择部分的第二行 -->
				<view class="time_choose_col" style="">
					<view  class="time_choose_first" style="" @click="to_place_choice">
						<view class=""  style="color:#999; font-size: 3rpx;">
							取车地点
						</view>
						<view class="" style="font-weight: 700; font-size: 40rpx;">
							{{place_choice}}
							<uni-icons type="location-filled" size="20"></uni-icons>
						</view>						
					</view>
				</view>
				<!-- 时间选择部分的第三行 -->
				<view v-if="if_show_return" class="time_choose_col" style="display: flex; justify-content: space-between;">
					<view class="time_choose_first" style="width: 30%;" @click="to_city_choice_return">
						<view class="" style="color:#999; font-size: 3rpx; width: 100%;">
							还车城市
						</view>
						<view class=""style="font-weight: 700; font-size: 40rpx; width: 100%;">
							{{return_city_choice}}
						</view>
					</view >					
				</view>
				<!-- 时间选择部分的第四行 -->
				<view v-if="if_show_return" class="time_choose_col" style="">
					<view  class="time_choose_first" style="" @click="to_place_choice_return">
						<view class=""  style="color:#999; font-size: 3rpx;">
							还车地点
						</view>
						<view class="" style="font-weight: 700; font-size: 40rpx;">
							{{return_place_choice}}
							<uni-icons type="location-filled" size="20"></uni-icons>
						</view>						
					</view>
				</view>
				<!-- 时间选择部分的第五行 -->
				<view class="time_choose_col" style="height: 100rpx;"@click="to_time_choice">
					<view class="time_choose_second" style="width: 33%;">
						<view class="" style="font-size: 35rpx;font-weight: 700;width: 100%;text-align: center; align-items: center;" v-model:initial_month="initial_month" v-model:initial_day="initial_day">{{initial_month}}月  {{initial_day}}日</view>
						<view class="" style="width: 100%;text-align: center; align-items: center;" v-model:initial_hour="initial_hour" v-model:initial_minute="initial_minute" v-model:initial_weekday="initial_weekday">{{initial_weekday}} {{initial_hour}}:{{initial_minute}}</view>
					</view>
					<view class="time_choose_second" style="width: 33%; ">
						<view class="" style="color: #999; width: 100%;text-align: center; align-items: center;">租期</view>
						<view class="" style="color: #999; width: 100%;text-align: center; align-items: center;"v-model:lease_term="lease_term">{{lease_term}}</view>
					</view>
					<view class="time_choose_second" style="width: 33%;">
						<view class="" style="font-size: 35rpx;font-weight: 700;width: 100%;text-align: center; align-items: center;"v-model:end_month="end_month" v-model:initial_day="end_day">{{end_month}}月  {{end_day}}日</view>
						<view class="" style="width: 100%;text-align: center; align-items: center;" v-model:end_hour="end_hour" v-model:end_minute="end_minute" v-model:end_weekday="end_weekday">{{end_weekday}} {{end_hour}}:{{end_minute}}</view>
					</view>
				</view>					
				<!-- 时间选择部分的第六行 -->
				<view class="time_choose_col">
					<view class="" @click="go_to_carList" style="font-size:20rpx; 80rpx; border-radius: 40rpx; width: 90%; margin: 0 auto; text-align:center; line-height: 80rpx; color: white; background-color:#ff9933;">
						马上选车
					</view>
				</view>				
			</view>		
		</view>
		
		<!-- 索引部分 -->
		<view class="index">
			<navigator url="../coupon/coupon" style="width: 40%; height: 310rpx; ">				
				<image src="../../static/lingquanzhongxin.png" style="width: 100%;height: 310rpx;" mode=""></image>
			</navigator>
			<view class="" style="width: 58%;height: 310rpx; display: flex; flex-direction: column; justify-content: space-between;">
				<navigator url="../invite/invite"style="width: 100%;height: 105rpx;"><image src="../../static/yaoqingyouli.png" style="width: 100%;height: 105rpx;" mode=""></image></navigator>
				<view class="" style="display: flex; justify-content: space-between;">
					<navigator url="../long_rent/long_rent"style="width: 49%;height: 200rpx;background-color:#FCBD71;"><image src="../../static/chaozhichangzu.png" style="width: 100%;height: 200rpx;" mode=""></image></navigator>
					<navigator url="../share/share"style="width: 49%;height: 200rpx;background-color:#C0C4CC;"><image src="../../static/chengweichezhu.png" style="width: 100%;height: 200rpx;" mode=""></image></navigator>
				</view>
			</view>
		</view>
		
		<!-- 新手指引部分 -->
		<navigator class="novice_guide" url="../guide/guide">
			<image src="../../static/xinshouzhiyin.png" style="width: 100%;height: 200rpx;" mode=""></image>
		</navigator>	
		
		<!-- 三重保障部分 -->
		<view class="three_guarantee">
			<view class="" style="font-size: 35rpx; font-weight: 800;  width: 100%;  text-align: center; line-height: 100rpx; height: 100rpx;">
				3重保障您的出行
			</view>
			<view class="" style="display: flex;width: 100%;">
				<view class="each_gurantee" >
					<uni-icons class="each_gurantee_icon" type="checkmarkempty"size="30" color="rgb(255,191,147)"></uni-icons>
					<view class="guarantee_content" >
						<view class="guarantee_content_title">
							立即确认
						</view>
						<view class="guarantee_content_text">
							无需等待
						</view>
					</view>
				</view>
				<view class="each_gurantee">
					<uni-icons class="each_gurantee_icon"  type="headphones" size="30" color="rgb(255,191,147)"></uni-icons>
					<view class="guarantee_content">
						<view class="guarantee_content_title">
							专业客服
						</view>
						<view class="guarantee_content_text">
							24小时在线
						</view>
					</view>
				</view>
				<view class="each_gurantee">
					<uni-icons class="each_gurantee_icon" type="heart-filled" size="30" color="rgb(255,191,147)"></uni-icons>
					<view class="guarantee_content">
						<view class="guarantee_content_title">
							退赔安心
						</view>
						<view class="guarantee_content_text">
							携程平台保障
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import selectSwitch from "@/components/xuan-switch/xuan-switch.vue";
	export default {		
		components: {
		
		selectSwitch
		
		},
	    data() {
	        return {
				initial_year:'',
				initial_month:'',
				initial_day:'',
				initial_hour:'',
				initial_minute:'',
				initial_weekday:'',
				end_year:'',
				end_month:'',
				end_day:'',
				end_hour:'',
				end_minute:'',
				end_weekday:'',
				lease_term:'',
				city_choice:'',
				place_choice:'',
				return_city_choice:'',
				return_place_choice:'',
				if_show_return:0,
				// 轮播图的内容
	            info: [{
	                url:'../../static/轮播1.png'
	            }, {
	                 url:'../../static/轮播2.png'
	            }, {
	                url:'../../static/轮播3.png'
	            }, {
	                 url:'../../static/轮播4.png'
	            }, {
	                 url:'../../static/轮播5.png'
	            }],
	            current: 0,
				// 轮播点的模型
	            mode: 'dot',
				// 轮播点的样式
				dotsStyles:{
					bottom:30,					
				},
				// 上门送取车的单选框
				value: -1,
				range: [{"value": 0,"text": "上门送取车"}],		
				//展示提醒取车的事项
				show_time_of_take_car: false,
				// 开关的内容
				switchList:[
					' ',
					' '
				],		
				// 开关颜色
				checked_bj_color:"#999",
				// 轮播图样式
				swiper_style:'',
				// 优惠券弹窗的变量
				show_toast: false,
				// 协议弹窗
				contentlist:[
					'wdaskjdhaskdhsddddddddddddddddddddddddddddddddddddddddddddaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa ',
					'asdasdasd ',
					'asdasdasd ',	
					'hhhhhh '	
					
				],
				
				show_toast_agreement: false
	        }
	    },		
		onLoad()
		{// 初始化：时间选择
			let date = new Date();
			date.setDate(date.getDate()+1);
			date.setHours(10);
			date.setMinutes(0);
			date.setSeconds(0);
			this.initial_month=date.getMonth()+1
			this.initial_day=date.getDate()
			this.initial_hour=date.getHours()
			this.initial_minute=date.getMinutes()
			this.initial_weekday=''
			// 初始化：两天后换车
			var temp =new Date(date.getTime()+172800000)
			this.end_month=temp.getMonth()+1
			this.end_day=temp.getDate()
			this.end_hour=temp.getHours()
			this.end_minute=temp.getMinutes()
			this.end_weekday=''
			if(this.initial_hour<10){this.initial_hour='0'+this.initial_hour;}			
			if(this.initial_minute<10){this.initial_minute='0'+this.initial_minute;}
			if(this.initial_month<10){this.initial_month='0'+this.initial_month;}
			if(this.initial_day<10){this.initial_day='0'+this.initial_day;}
			if(this.end_hour<10){this.end_hour='0'+this.end_hour;}			
			if(this.end_minute<10){this.end_minute='0'+this.end_minute;}
			if(this.end_month<10){this.end_month='0'+this.end_month;}
			if(this.end_day<10){this.end_day='0'+this.end_day;}
			this.lease_term='2天0小时'	
			
			// 优惠卷弹窗初始化
			this.show_toast=true;
			// 协议弹窗初始化
			this.show_toast_agreement=true;
			
		},
		onShow(){			
			this.if_show_return = 0;						
			
			this.city_choice = getApp().globalData.city_choice;
			this.place_choice = getApp().globalData.place_choice;	
			this.return_city_choice = getApp().globalData.city_choice_return;
			this.return_place_choice = getApp().globalData.place_choice_return;				
			// 协议弹窗加空格
			let agreement_list=this.contentlist;
			for(let i=0;i<agreement_list.length;i++)
			{
				agreement_list[i]='\xa0\xa0\xa0'+agreement_list[i];
			}
		},
		
	    methods: {
			// 轮播图触发change时调用
	        swiper_change(e) {
	            this.current = e.detail.current;
	        },
			// check_change(e){
			// 	this.show_time_of_take_car = !this.show_time_of_take_car;
			// },
			// 异地还车change时调用
			changeSwitch(isSwitch)
			{
				let that = this;
				if(isSwitch)
				{
					this.checked_bj_color="#999";
					this.if_show_return = 0;					
				}
				else
				{					
					this.checked_bj_color="rgb(25,137,250)";
					this.return_city_choice = this.city_choice;
					this.return_place_choice = this.place_choice;
					this.if_show_return = 1;					
				}
			},
			// 跳转到时间选择页面
			to_time_choice()
			{
				let that = this;
				uni.navigateTo({
					url:'../time_choice/time_choice',
					  events: {
					    // 为指定事件添加一个监听器，获取被打开页面传送到当前页面的数据
					    from_timeChoic_to_mainPage: function(from_time_choice) {
					        that.initial_day = from_time_choice.initial_day;
					        that.initial_month = from_time_choice.initial_month;
					        that.initial_hour = from_time_choice.initial_hour;
					        that.initial_minute = from_time_choice.initial_minute;
					        that.end_day = from_time_choice.end_day;
					        that.end_month = from_time_choice.end_month;
					        that.end_hour = from_time_choice.end_hour;
					        that.end_minute = from_time_choice.end_minute;
					        that.lease_term=from_time_choice.lease_term;
					      },					   					  
					  },
					  success: function(res) {
					    // 通过eventChannel向被打开页面传送数据
					    res.eventChannel.emit('from_mainPage_to_timeChoice', {
							initial_day:that.initial_day,
							initial_month:that.initial_month,
							initial_hour:that.initial_hour,
							initial_minute:that.initial_minute,
							end_day:that.end_day,
							end_month:that.end_month,
							end_hour:that.end_hour,
							end_minute:that.end_minute,
							lease_term:that.lease_term
						})
					  }
				})
			},
			to_city_choice(){
				let that = this;
				
				uni.navigateTo({
					url:'../city_choice/city_choice',
					  success: function(res) {		
						  // 通过eventChannel向被打开页面传送数据
						  // res.eventChannel.emit('from_mainPage_to_cityChoice', {
						  // 	is_from_main:1
						  // })
						  getApp().globalData.is_from_main = 1;						 
					  }
				})				
			},
			to_place_choice(){
				let that = this;
				uni.navigateTo({
					url:'../place_choice/place_choice',
					success: function(res) {
						  // 通过eventChannel向被打开页面传送数据
						  // res.eventChannel.emit('from_mainPage_to_cityChoice', {
						  // 	is_from_main:1
						  // })
						  getApp().globalData.is_from_main = 1;						  
					}
				})	
			},
			to_place_choice_return()
			{
				uni.navigateTo({
					url:'../place_choice/place_choice',
					success: function(res) {
					  // 通过eventChannel向被打开页面传送数据
					  // res.eventChannel.emit('from_mainPage_to_cityChoice', {
					  // 	is_from_main:1
					  // })
					  getApp().globalData.is_from_main_return = 1;
					}
				})
			},
			to_city_choice_return(){
				let that = this;
				uni.navigateTo({
					url:'../city_choice/city_choice',
					  success: function(res) {		
						  // 通过eventChannel向被打开页面传送数据
						  // res.eventChannel.emit('from_mainPage_to_cityChoice', {
						  // 	is_from_main:1
						  // })
						  getApp().globalData.is_from_main_return = 1;
					  }
				})				
			},
			go_to_carList()
			{
				uni.navigateTo({
					url:"../carList/carList"
				})
			},
			delete_toast()
			{
				this.show_toast=false;
			},
			not_show_toast()
			{
				uni.navigateTo({
					url:'../coupon/coupon'
				})
				this.show_toast=false;
			},
			go_to_main(){
				this.show_toast_agreement=false;
				
			},
			exit_agreement(){
				uni.showToast({
					icon:'error',
					title:'请先同意协议'
				})
			}
			
	    }
	}
</script>

<style>
	.each_gurantee{
		width: 33%;
		display: flex;
	}
	.guarantee_content_title{
		font-size: 30rpx;
	}
	.guarantee_content_text{
		font-size: 8rpx;
		color: #999;
	}
	.time_choose{
		width: 90%; 
		background-color: white; 	
		margin: 0 auto; 
		position: relative;
		top: -50rpx;
		border-radius: 10rpx;
		border: 1rpx #eee8e3 solid;
		box-shadow: 1rpx 1rpx 10rpx #EEE8E3;
	},
	.novice_guide{
		width: 90%;
		margin: 0 auto;
		margin-top: 20rpx;
		height: 200rpx;
	},
	.three_guarantee{
		width: 90%;
		margin: 0 auto;
		/* background-color: rgb(244,244,244); */
		background-color: rgb(254,242,183);
		margin-top: 50rpx;
		padding-bottom: 30rpx;
	}
	.index{
		width: 90%;
		margin: 0 auto;
		display: flex;
		justify-content: space-between;
		border-radius: 10rpx;		
		box-shadow: 1rpx 1rpx 10rpx #EEE8E3;
	},
	.time_choose_col{
	width: 100%; 
	display: flex;
	margin-bottom: 10rpx;
	}

	.swiper-item navigator image{
		display: block;
		height: 400rpx;
		width: 100%;	
	}
	
	.swiper_top{		
		 height: 400rpx; 		
	}
	.swiper-box{
		height: 400rpx;
	}
	.title-box{
			background-color: #FFFFFF;
			width: 100%;
			height: 100rpx;
			border-bottom: 1rpx solid #000000;
		}
		.title{
			font-size: 40rpx;
			line-height: 100rpx;
			text-align: center;
		}
		.content{
			word-wrap: break-word;
		}
		.button-box{
			width: 100%;
			background-color: #FFFFFF;
			display: flex;
			flex-wrap: nowrap;
		}
		.agree{
			width: 25%;
			background-color: #FF5500;
			color: #FFFFFF;
			margin-bottom: 20rpx;
		}
		.dissagree{
			width: 25%;
			background-color: #FFFFFF;
			color: #555555;
			margin-bottom: 20rpx;
		}
</style>
