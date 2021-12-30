<template>
	<view>

		
		<!-- 地址搜索栏 -->		
		<u-sticky offset-top="0" ref="search" id="search" v-if="!is_website">
			<view class="__bdi" style="background-color: white;">
				<view class="" style="display: flex;width: 90%;  margin: 0 auto; height: 60rpx;">
					<view class=""style="overflow: hidden; width: 10%;height:60rpx; line-height:60rpx; " @click="to_city_choice">
						{{city_choice}}
					</view>
					<view class="" style="width:10%;height:60rpx; line-height:60rpx; "@click="to_city_choice">▼
					</view>
					<input  style="width: 80%;height: 60rpx;" type="text" placeholder="地址/街道/酒店名/景点名" placeholder-class="placeholder_style">				
				</view>			
			</view>
		</u-sticky>
		<!-- 地址栏 -->
		<view class="" v-if="!is_website">
			<view class="" v-for="each_type in all_place" style=" width: 90%; margin: 0 auto;  margin-top: 30rpx;">
				<!-- 标题 -->
				<view class="" style="font-weight: 700;font-size: 30rpx;">
					{{each_type.type}}
				</view>
				<view class="" style="" >
					<u-tag v-for="item in each_type.place" :text="item" @click="back_to_main(item)" style="width: 33%;margin-right: 2rpx; background-color: white;border: none; color: #000000;"/>	
				</view>
					
			</view>
		</view>			
	</view>
</template>

<script>
	export default {
		data() {
			return {
				place_type:'',
				each_place:'',
				is_website:0,
				city_choice:'',
				website_left_style:'width:30%;',
				website_right_style:'width:70%',
				all_place:[
					{   
						id:'0',
						type:'机场',
						place:[
							'国际机场',
							'白云机场',
							'黑云机场',
							'红云机场',
							'绿云机场'
						]
					},
					{
						id:'1',
						type:'火车站',
						place:[
							'北京南站',
							'北京东站',
							'北京北站',
							'北京西站',							
						]
					},
					{
						id:'2',
						type:'热门地区',
						place:[
							'宋家庄',
							'五棵松',
							'圆明园',
							'大学城',
							'广州塔'
						]
					},
					{
						id:'3',
						type:'商圈',
						place:[
							'珠江新城',
							'丽影广场',
							'北京路商业步行街'
						]
					},
					{
						id:'3',
						type:'商圈',
						place:[
							'珠江新城',
							'丽影广场',
							'北京路商业步行街'
						]
					},
					{
						id:'3',
						type:'商圈',
						place:[
							'珠江新城',
							'丽影广场',
							'北京路商业步行街'
						]
					},
					{
						id:'3',
						type:'商圈',
						place:[
							'珠江新城',
							'丽影广场',
							'北京路商业步行街'
						]
					},
					{
						id:'3',
						type:'商圈',
						place:[
							'珠江新城',
							'丽影广场',
							'北京路商业步行街'
						]
					},
					{
						id:'3',
						type:'商圈',
						place:[
							'珠江新城',
							'丽影广场',
							'北京路商业步行街'
						]
					},{
						id:'3',
						type:'商圈',
						place:[
							'珠江新城',
							'丽影广场',
							'北京路商业步行街'
						]
					},
					{
						id:'3',
						type:'商圈',
						place:[
							'珠江新城',
							'丽影广场',
							'北京路商业步行街'
						]
					},
					{
						id:'3',
						type:'商圈',
						place:[
							'珠江新城',
							'丽影广场',
							'北京路商业步行街'
						]
					}
				],				
			}
		},
		onLoad(e){					
		},
		onShow(){
			this.city_choice = getApp().globalData.city_choice;
			
		},
		onReady()
		{		
		},
		methods: {
			change_to_place()
			{
				this.is_website = 0;
			},
			change_to_website()
			{
				this.is_website = 1;
				// let top = this.$refs.top;
				// let search = this.$refs.search;
				
				// let change_height = setInterval(function(){					
				// 	if(website_left!=null&&website_right!=null)
				// 	{
				// 		console.log("success!!!!!");
				// let website_left = document.getElementById("website_left");
				// let website_right = document.getElementById("website_right");
				// 		console.log(top.clientHeight+search.clientHeight);
				// 		website_left.style.height = screen.height-(top.clientHeight+search.clientHeight);
				// 		website_right.style.height = screen.height-(top.clientHeight+search.clientHeight);					
				// 		clearInterval(change_height);
				// 	}
				// },1000);
							
			},
			to_city_choice()
			{
				let that = this;
				uni.redirectTo({
					url:'../city_choice/city_choice',
					  success: function(res) {			
						  getApp().globalData.is_from_place = 1;
						  // 通过eventChannel向被打开页面传送数据
						  // res.eventChannel.emit('from_placeChoice_to_cityChoice', {
						  // 	is_from_place:1
						  // })
					  }
				})	
			},
			back_to_main(item){
				if(getApp().globalData.is_from_main==1)
				{
					getApp().globalData.place_choice = item;
					uni.switchTab({
						url:"../mian_page/mian_page",					
					})	
					getApp().globalData.is_from_main=0;
				}
				else if(getApp().globalData.is_from_main_return==1)
				{
					getApp().globalData.place_choice_return = item;
					uni.switchTab({
						url:"../mian_page/mian_page",					
					})	
					getApp().globalData.is_from_main_return=0;
				}
			}
		}
	}
</script>

<style>
	.top_style{
		width: 100%;
		height: 60rpx;
		line-height: 60rpx;
		text-align: center;
		font-size: 30rpx;	
	}
	.choosing{
		background-color: orange;
		color: white;
		border: 1rpx orange solid;
	}
	.not_choosing{
		background-color: white;
		color: black;
		border: 1rpx solid #eeeeee;
	}
</style>
