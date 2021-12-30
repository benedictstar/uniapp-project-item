<template>
	<view>
		<!-- 顶部选择栏 -->
		<u-sticky ref="top" id="top">		
				<view class="" style="width: 100%; background-color: white;">
					<view class="" style="display: flex; width: 90%; margin: 0 auto; border-radius: 10rpx;  ">
						<view class="top_style" @click="change_to_place" :class="{'choosing':!is_website,'not_choosing':is_website}">
							地址
						</view>
						<view class="top_style"  @click="change_to_website" :class="{'choosing':is_website,'not_choosing':!is_website}">
							网点
						</view>
					</view>
				</view>				
		</u-sticky>
		
		<!-- 地址搜索栏 -->		
		<u-sticky offset-top="60" ref="search" id="search" v-if="!is_website">
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
		<!-- 网点搜索栏 -->
		<u-sticky offset-top="60" v-if="is_website">
			<view class="__bdi" style="background-color: white;">
				<view class="" style="display: flex;width: 90%;  margin: 0 auto; height: 60rpx;">
					<view class=""style="overflow: hidden; width: 10%;height:60rpx; line-height:60rpx; " @click="to_city_choice">
						{{city_choice}}
					</view>
					<view class="" style="width:10%;height:60rpx; line-height:60rpx; "@click="to_city_choice">▼
					</view>
					<input  style="width: 80%;height: 60rpx;" type="text" placeholder="输入地址搜索周边网点" placeholder-class="placeholder_style">				
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
		<!-- 网点栏 -->
		<u-sticky offset-top="120">
			<view class="" ref="website"  v-if="is_website" style="display: flex;">
			<!-- 网点栏左边的区 -->
			<view class="" id="website_left" :style="website_left_style">
				<view class="" style="height: 100rpx; width: 100%; line-height: 100rpx; text-align: center;" v-for="item in all_self_help ">
					{{item.area}}
				</view>
			</view>
			<!-- 网点栏右边的服务点 -->
			<view class="" id="website_right" :style="website_right_style">
				<view class="" style=" width: 100%;" v-for="items in all_self_help ">
					<!-- 哪个区 -->
					<view class="" style="color:#7e7e7e;background-color: #f4f4f4;">
						{{items.area}}
					</view>
					<view class="" style="width: 100%;" v-for="it in items.self_help">
						<!-- 哪个自助点 -->
						<view class="" style="padding-top: 5rpx; padding-bottom: 5rpx; font-size: 30rpx;width: 90%; margin: 0 auto;">
							{{it.self_help_name}}
						</view>
						<!-- 哪个自助点的介绍 -->
						<view class="" style="color: #999;; padding-top: 5rpx; padding-bottom: 5rpx;width: 90%; margin: 0 auto;">
							{{it.self_help_map}}
						</view>
					</view>
				</view>
			</view>
		</view>
	</u-sticky>
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
				all_self_help:[
					{
						area:'石景山区',
						self_help:[
							{
								self_help_name:'首都机场',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'国贸服务点',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'望京服务点',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'芍药居服务点',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'北沙滩服务点',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'四惠服务点',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							}														
						],						
					},
					{
						area:'西城区',
						self_help:[
							{
								self_help_name:'首都机场2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'国贸服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'望京服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'芍药居服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'北沙滩服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'四惠服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							}														
						],						
					},
					{
						area:'北城区',
						self_help:[
							{
								self_help_name:'首都机场3',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'国贸服务点3',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'望京服务点3',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'芍药居服务点3',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'北沙滩服务点3',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'四惠服务点3',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							}														
						],						
					},
					{
						area:'东城区',
						self_help:[
							{
								self_help_name:'首都机场4',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'国贸服务点4',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'望京服务点4',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'芍药居服务点4',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'北沙滩服务点4',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'四惠服务点4',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							}														
						],						
					},
					{
						area:'南景山区',
						self_help:[
							{
								self_help_name:'首都机场',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'国贸服务点',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},							
							{
								self_help_name:'北沙滩服务点',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'四惠服务点',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							}														
						],						
					},
					{
						area:'西城区',
						self_help:[
							{
								self_help_name:'首都机场2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'国贸服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'望京服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'芍药居服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'北沙滩服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'四惠服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							}														
						],						
					},
					{
						area:'大学城区',
						self_help:[
							
							{
								self_help_name:'北沙滩服务点',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'四惠服务点',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							}														
						],						
					},
					{
						area:'番禺区',
						self_help:[
							{
								self_help_name:'首都机场2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							{
								self_help_name:'国贸服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							},
							
							{
								self_help_name:'北沙滩服务点2',
								self_help_map:'首都机场1号航楼出发层靠右执行100米左右，之后就是直走1000米，向后899米'
							}													
						],						
					}
				]
			}
		},
		onLoad(e){					
		},
		onShow(){
			this.city_choice = getApp().globalData.city_choice;
			
		},
		onReady()
		{
			let top = document.getElementById("top");
			let search = document.getElementById("search");
			let window_height = 0;
			uni.getSystemInfo({
			    success: function (res) {		
					// 获取可用空间的高度(屏幕高度-状态栏高度-导航栏高度)
			      console.log("windowHeight： "+res.windowHeight);				
			      window_height = res.windowHeight;		      
			    }
			});
			// 将单位为px的数值转换为单位为rpx
			window_height = window_height * 750 / uni.getSystemInfoSync().windowWidth;
			let top_clientHeight = top.clientHeight * 750 / uni.getSystemInfoSync().windowWidth;
			let search_clientHeight = search.clientHeight * 750 / uni.getSystemInfoSync().windowWidth;
			let website_height =window_height-(top_clientHeight+ search_clientHeight);
			
			this.website_left_style+="color:#7e7e7e;background-color: #f4f4f4;overflow:scroll;"
			this.website_left_style+= "height:"+website_height+"rpx";
			this.website_right_style+="background-color:yellow;overflow:scroll;"
			this.website_right_style+= "height:"+website_height+"rpx";
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
				getApp().globalData.place_choice = item;
				uni.switchTab({
					url:"../mian_page/mian_page",					
				})	
			}
		}
	}
</script>

<style>
	.top_style{
		width: 50%;
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
