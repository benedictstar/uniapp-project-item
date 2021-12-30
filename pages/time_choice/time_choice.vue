<template>
	<view>
		<!-- 顶部的用车时间条 -->
		<view class="time_choose_show" style="height: 100rpx;">
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
		<!-- 日历选择器 -->
    	<view class="" style="height: 650rpx; width: 100%; margin-bottom: 150rpx;">			
			<cal
			    
				:lunar="lunar"
				isFixed
				:minDate="minDate"
				:maxDate="maxDate"
				:btnType="btnType"
				:activeBgColor="activeBgColor"
				:rangeBgColor="rangeBgColor"
				:rangeColor="rangeColor"
				:startText="startText"
				:endText="endText"
				:arrowType="arrowType"
				:type="type"
				:initStartDate="initStartDate"
				:initEndDate="initEndDate"
				ref="calendar"
				@has_click="time_change"
			></cal>
		</view>	
		<!-- 时间滚轮 -->
		<view class="" style="height: 300rpx;  width: 100%; margin-bottom: 25rpx;">
			<view class="" style=" display: flex; justify-content: space-between;">
				<view class=""  style="width: 50%; font-weight: 800; font-size: 30rpx; text-align: center; line-height: 40rpx; height: 40rpx;">
					取车时间
				</view>
				<view class="" style=" width: 50%; font-weight: 800; font-size: 30rpx; text-align: center; line-height: 40rpx; height: 40rpx;">
					还车时间
				</view>
			</view>
			<view class="" style="display: flex; justify-content: space-around;height: 300rpx; overflow: hidden; ">				
				<view class="" style="width: 48%;">
					<my_picker :list="all_hour" :default-value="initial_take" @DateChange="time_of_take"></my_picker>		
				</view>
				<view class="" style="width: 48%;">
					<my_picker :list="all_hour" :default-value="initial_return" @DateChange="time_of_return"></my_picker>		
				</view>
			</view>			
		</view>
		<!-- 确定 -->
		<view class="" @click="to_main_page" style="margin-top: 100rpx; border-radius: 15rpx; line-height: 100rpx; text-align: center; height: 100rpx; width: 90%; margin: 0 auto; margin-bottom: 10rpx; color: white; background-color: orange;">
			确定
		</view>
	</view>
</template>

<script>
import cal from "../../components/time_choice_cal/time_choice_calendar.vue"	
import my_picker from "../../components/time_choice_picker/time_choice_picker.vue"
	export default {
		
		data() {
			//设置小时数数组
			let hours_temp = ['00','01','02','03','04','05','06','07','08','09','10','11','12','13']
			//设置分钟数数组
			let minutes_temp = ['00','15','30','45']			
			let all_hour = []
			let value = 1;
			for(let i=0;i<24;i++)
			{
				for(let j=0;j<minutes_temp.length;j++)
				{
					if(i<10)
					{
						let temp=hours_temp[i]+":"+minutes_temp[j];
						let each_temp = new Object();
						each_temp.value = value.toString();
						each_temp.label = temp;
						all_hour.push(each_temp);
					}
					else{
						let temp=i+":"+minutes_temp[j];
						let each_temp = new Object();
						each_temp.value = value.toString();
						each_temp.label = temp;
						all_hour.push(each_temp);
					}
					
					value++;
				}
				
			}
			
			return {
				// 显示时间的相关参数
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
				lease_term:'0天0小时',
				// 日历的相关参数
				type: 1,
				status: [],
				arrowType: 1,
				minDate: '',
				maxDate: '',
				btnType: 'primary',
				activeBgColor: '',
				rangeBgColor: '',
				rangeColor: '',
				startText: '',
				endText: '',
				lunar: true,
				result: '',
				lunarResult: '',
				initStartDate: '',
				initEndDate: '',
				
				// picker的相关参数
				all_hour:all_hour,
				initial_take:[0],
				initial_return:[0]
			}
		},
		components:{
			cal,
			my_picker
		},
		onShow(e){
			// 小时和分钟初始化
			this.initial_hour='00';
			this.initial_minute='00';
			this.end_hour='00';
			this.end_minute='00';
			
			  let that = this;			
			  const eventChannel = this.getOpenerEventChannel()			  	 
			  // 监听acceptDataFromOpenerPage事件，获取上一页面通过eventChannel传送到当前页面的数据
			  eventChannel.on('from_mainPage_to_timeChoice', function(from_main_page) {
				that.initial_day = from_main_page.initial_day;
				that.initial_month = from_main_page.initial_month;
				that.initial_hour = from_main_page.initial_hour;
				that.initial_minute = from_main_page.initial_minute;
				that.end_day = from_main_page.end_day;
				that.end_month = from_main_page.end_month;
				that.end_hour = from_main_page.end_hour;
				that.end_minute = from_main_page.end_minute;
				that.lease_term=from_main_page.lease_term;
			  })
			  // 日历的初始化
			  this.arrowType = 1;
			  this.minDate = '1920-01-01';
			  this.maxDate = '2099-12-12';
			  this.btnType = 'primary';
			  this.activeBgColor = '#ff9933';
			  this.rangeBgColor = 'rgba(255, 153, 51,0.1)';
			  this.rangeColor = '#ff9933';
			  this.startText = '开始';
			  this.endText = '结束';		
			  this.type = 2;
			  this.initStartDate = new Date().getFullYear()+'-'+this.initial_month+'-'+this.initial_day;
			  this.initEndDate = new Date().getFullYear()+'-'+this.end_month+'-'+this.end_day;
			  // picker选择器的初始化
			  this.initial_take[0]=4*this.initial_hour+this.initial_minute/15;
			  this.initial_return[0]=4*this.end_hour+this.end_minute/15;
		},
		methods: {
			// 日历时间变化时调用
			time_change(e)
			{
				var weekday=new Array(7)
				weekday[0]="周日"
				weekday[1]="周一"
				weekday[2]="周二"
				weekday[3]="周三"
				weekday[4]="周四"
				weekday[5]="周五"
				weekday[6]="周六"
								
				let initial = e.start_time.split('-');
				let end = e.end_time.split('-');
				this.initial_year =  initial[0];
				this.initial_month = initial[1];
				this.initial_day = initial[2];
				this.initial_weekday = weekday[new Date(e.start_time).getDay()];
				this.end_year = end[0];
				this.end_month = end[1];
				this.end_day = end[2];
				if(this.initial_month<10)
				{
					this.initial_month = '0'+this.initial_month;
				}
				if(this.initial_day<10)
				{
					this.initial_day = '0'+this.initial_day;
				}
				if(this.end_month<10)
				{
					this.end_month = '0'+this.end_month;
				}
				if(this.end_day<10)
				{
					this.end_day = '0'+this.end_day;
				}
				this.end_weekday = weekday[new Date(e.end_time).getDay()];
				this.compute_lease_term();
			},
			// 取车时间变化时调用
			time_of_take(hour,minute)
			{				
				this.initial_hour = hour;
				if(hour<10){this.initial_hour='0'+hour;}
				this.initial_minute = minute;	
				if(minute==0){this.initial_minute='0'+minute;}
				this.compute_lease_term();
			},
			// 还车时间变化时调用
			time_of_return(hour,minute)
			{
				this.end_hour = hour;
				if(hour<10){this.end_hour='0'+hour;}
				this.end_minute = minute;
				if(minute==0){this.end_minute='0'+minute;}
				this.compute_lease_term();
			},
			// 计算租期
			compute_lease_term()
			{
				let millisecond_lease_term=new Date(this.end_year+'-'+this.end_month+'-'+this.end_day+' '+this.end_hour+':'+this.end_minute)-new Date(this.initial_year+'-'+this.initial_month+'-'+this.initial_day+' '+this.initial_hour+':'+this.initial_minute);
				if(millisecond_lease_term>0)
				{
					let lease_term_day = Math.floor((millisecond_lease_term) / (86400000)); //天
					let lease_term_hours = Math.floor((millisecond_lease_term % 86400000) / 3600000); //时
					this.lease_term = lease_term_day+'天'+lease_term_hours+'小时';
				}
				else{
					let lease_term_day = 0; //天
					let lease_term_hours =0; //时
					this.lease_term = lease_term_day+'天'+lease_term_hours+'小时';
				}				
			},
			to_main_page()
			{
				const eventChannel = this.getOpenerEventChannel()
				let that = this;
				eventChannel.emit('from_timeChoic_to_mainPage', {
					initial_day:that.initial_day,
					initial_month:that.initial_month,
					initial_hour:that.initial_hour,
					initial_minute:that.initial_minute,
					end_day:that.end_day,
					end_month:that.end_month,
					end_hour:that.end_hour,
					end_minute:that.end_minute,
					lease_term:that.lease_term					
				});	
				uni.switchTab({
					url:"../mian_page/mian_page",					
				})			
			}
		}
	}
</script>

<style>
.time_choose_show{
	margin-top: 20rpx;
	display: flex;
	width: 100%;
	justify-content: space-between;	
}
</style>
