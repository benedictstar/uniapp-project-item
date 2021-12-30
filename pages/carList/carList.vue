<!-- 车辆列表页 -->
<template>
	<view>
		<!-- 导航栏 -->
		<view class="nav">
			<view class="nav-search">
				<!-- 搜索框 -->
				<!-- <u-search
					placeholder="全部品牌/车型"
					:show-action="false"
					input-align="center"
					bg-color="#fff"
					border-color="#e0dee1"
					v-model="keyword"
					@change="doSomething"
				></u-search> -->
				<!-- 搜索框 -->
				<u-search
					placeholder="全部品牌/车型"
					:show-action="false"
					:disabled="true"
					input-align="center"
					bg-color="#fff"
					border-color="#e0dee1"
					@click="toSearchDetails"
					:change="search_change"
					:search="search_search"				
				></u-search>
			</view>
			<view class="" style="display: flex; justify-content: space-around;">
				<!-- 地点和时间选择按钮 -->		
				<view class="place_and_time" @click="choose_place">{{ carPos }}</view>						
				<view class="place_and_time" >{{ carTime }}</view>	
				<u-button @click="toFilter"  class="place_and_time" style="margin-left: 0rpx; margin-right: 0rpx;" type="warning" shape="circle" :class="{notActive:isNotActive}">筛选<u-badge  :offset="[-10,-10]" type="error" :count="list_length"></u-badge></u-button>				<!-- filterCount	 -->		
			</view>
			<view class="flex">
				<u-dropdown style="width:100%;">
					<u-dropdown-item v-model="value_sort" title="综合排序" :options="options_sort"></u-dropdown-item>
					<u-dropdown-item v-model="value_rent" title="租金" :options="options_rent"></u-dropdown-item>
					<u-dropdown-item v-model="value_car_type" title="车型" :options="options_car_type"></u-dropdown-item>
				</u-dropdown>
			</view>

			<view class="flex">
				<view @click="click_special_car"  :class="{'is_choose_filter':if_special_car,'not_choose_filter':!if_special_car}">
					特价车
				</view>
				<view @click="click_premium_car":class="{'is_choose_filter':if_premium_car,'not_choose_filter':!if_premium_car}">
					严选优车
				</view>
				<view @click="click_local_licence" :class="{'is_choose_filter':if_local_licence,'not_choose_filter':!if_local_licence}">
					<view>本地牌照</view>
				</view>
				<view @click="click_unlimited" :class="{'is_choose_filter':if_unlimited,'not_choose_filter':!if_unlimited}">
					<view>不限里程</view>
				</view>	
			</view>
			
		</view>
		<!-- 广告位 -->
		<navigator url="" style="margin-top: 20rpx;">
			<view class="">
				<image src="../../static/guanggao.png"  style="width: 100%; height: 200rpx;" mode="scaleToFill"></image>
			</view>
		</navigator>
		<!-- 商品列表 -->
		<view class="carList">
			<view class="goods_list">
					<view class="goods_item u-flex u-p-26" v-for="item in goodsList" :key="item.goods_sn" >								
							<u-image width="40%" height="260rpx" src="https://carphoto.atzuche.com/car/21/01/651916083/1611200319690_1.jpg" @click="go_to_car_detail"></u-image>
							<view class="words u-flex u-p-l-26 u-p-r-26" style="width:60%;	flex-direction:column;align-items:flex-start;height:260rpx;justify-content:space-between" @click="go_to_car_detail">
								<view class="keywords u-font-30 u-line-1">{{ item.keywords }}</view>
								<view class="otherwords u-font-20 u-flex u-row-between u-line-1 u-m-t-15" style="color:gray">
									<text >{{ item.license_number }}</text>
									<text>{{ item.distance }}km</text>
									<text>日均限{{ item.daily_milestone }}km</text>
								</view>
								<view class="tag u-font-20 u-flex u-row-between u-line-1 u-m-t-15">
									<text style="border:solid 1rpx;border-radius:25%">{{ item.tag[0] }} </text>
									<text class="u-m-l-8" style="border:solid 1rpx;border-radius:25%">{{ item.tag[1] }} </text>
									<text class="u-m-l-8" style="border:solid 1rpx;border-radius:25%">{{ item.tag[2] }} </text>
									<text class="u-m-l-8" style="border:solid 1rpx;border-radius:25%">{{ item.tag[3] }}</text>
								</view>
								<view class="discounts u-font-20 u-line-1 u-m-t-15" style="border:solid 1px orange;color:orange;border-radius:25%">{{ item.discounts }}</view>
								<view class="price u-font-26 u-line-1 u-p-t-15 u-flex">
									<view style="font-weight:600;flex:1 0" class="u-font-30">￥{{ item.price }}/天</view>
									<view style="color:grey;text-decoration:line-through;flex:1 1" class="u-font-12 u-p-l-12">￥{{ item.price + 200 }}/天</view>
								</view>
							</view>						
					</view>
				</view>
						
		</view>
	</view>
</template>

<script>
export default {
	onLoad() {
	},
	data() {
		return {
			keyword: '', //
			carTime: '不限时间', //用车时间
			carPos: '广州', //用车地点
			value_sort: 1,
			value_rent: 2,
			value_car_type: 3,

			options_sort: [
				{
					label: '综合排序',
					value: 1
				},
				{
					label: '价格最低',
					value: 2
				},
				{
					label: '价格最高',
					value: 3
				},
				{
					label: '距离最近',
					value: 4
				}
			],
			options_rent: [
				{
					label: '0-150',
					value: 1
				},
				{
					label: '150-250',
					value: 2
				},
				{
					label: '250-350',
					value: 3
				},
				{
					label: '350-以上',
					value: 4
				}
			],
			options_car_type: [
				{
					label: '热销',
					value: 2
				},
				{
					label: '特价车',
					value: 3
				},
				{
					label: '经济型',
					value: 4
				},
				{
					label: '舒适型',
					value: 5
				},
				{
					label: 'SUV',
					value: 6
				},
				{
					label: '商务型',
					value: 7
				},
				{
					label: '豪华型',
					value: 8
				},
				{
					label: '跑车',
					value: 9
				},
				{
					label: '新能源',
					value: 10
				}
			],
			
			// 判断是否已选中那四个筛选条件
			if_special_car:0,
			if_premium_car:0,
			if_local_licence:0,
			if_unlimited:0,
			current: 0,
			list_length:0,
			selectedTabs: [], //已选中的标签
			
			goodsList: [
					{
						goods_sn: 1,
						car_picture: 'https://carphoto.atzuche.com/car/21/01/651916083/1611200319690_1.jpg',
						keywords: '兰博基尼 Aventador 6.5L',
						license_number: '粤B***02',
						distance: 5.6,
						daily_milestone: 200,
						tag: ['支持送取', '信用双免', '安心保障', '收藏最多'],
						discounts: '满4000减300',
						price: 10193,
						ori_price: 10343
					},
					{
						goods_sn: 2,
						car_picture: 'https://carphoto.atzuche.com/car/21/01/651916083/1611200319690_1.jpg',
						keywords: '兰博基尼 Aventador 6.5L',
						license_number: '粤B***02',
						distance: 5.6,
						daily_milestone: 200,
						tag: ['支持送取', '信用双免', '安心保障', '收藏最多'],
						discounts: '满4000减300',
						price: 10193,
						ori_price: 10343
					},
					{
						goods_sn: 3,
						car_picture: 'https://carphoto.atzuche.com/car/21/01/651916083/1611200319690_1.jpg',
						keywords: '兰博基尼 Aventador 6.5L',
						license_number: '粤B***02',
						distance: 5.6,
						daily_milestone: 200,
						tag: ['支持送取', '信用双免', '安心保障', '收藏最多'],
						discounts: '满4000减300',
						price: 10193,
						ori_price: 10343
					}
				]
			
			
		};
	},
	onLoad(){
		
	},
	onShow()
	{
		// 城市赋初值
		this.carPos = getApp().globalData.city_choice_carList;
		
		// 筛选功能初始化
		let other_condition = getApp().globalData.filter[0];
		let license = getApp().globalData.filter[2];
		let limited = getApp().globalData.filter[4];
		// 筛选页面返回到这里时同步背景色
		if(license.groupContent[0].checked)
		{
			this.if_local_licence = 1;
			other_condition.groupContent[2].checked=true;		
		}
		else
		{
			this.if_local_licence = 0;
			other_condition.groupContent[2].checked=false;
		}
		if(limited.groupContent[0].checked)
		{
			this.if_unlimited = 1;
			other_condition.groupContent[3].checked=true;
		}
		else
		{
			this.if_unlimited = 0;
			other_condition.groupContent[3].checked=false;
		}		
		if(other_condition.groupContent[0].checked)
		{
			this.if_special_car=1;
		}
		else{
			this.if_special_car=0;
		}
		if(other_condition.groupContent[1].checked)
		{
			this.if_premium_car=1;
		}
		else{
			this.if_premium_car=0;
		}
		this.get_length_and_ans();
		
		// 输出搜索关键字
		let keyword = getApp().globalData.search_keyword;
		console.log("搜索关键字是"+keyword);
		
	},
	methods: {
		get_length_and_ans()
		{
			let filter = getApp().globalData.filter;
			let ans = [];
			let length=0;
			for(let i=1;i<filter.length;i++)
			{
				for(let j=0;j<filter[i].groupContent.length;j++)
				{
					let temp = filter[i].groupContent;
					if(temp[j].checked)
					{
						length++;
						ans.push(temp[j].name);
					}
				}
			}
			for(let j=0;j<2;j++)
			{
				let temp = filter[0].groupContent;
				if(temp[j].checked)
				{
					length++;
					ans.push(temp[j].name);
				}
			}
			this.list_length=length;
			this.selectedTabs = ans.slice(0);
			console.log("筛选长度是"+length);
			console.log("筛选内容是"+ans);
			
		},		
		doSomething() {
			console.log('搜索框内是:', this.keyword);
		},
		change(index) {
			this.current = index;
		},				
		toFilter(){
			this.$u.route('/pages/filter/filter', {
				filterNames: this.filterNames,
				realFilterNames:this.realFilterNames,
			});
		},		
		click_special_car()
		{
			let that = this;
			let array = getApp().globalData.filter[0].groupContent;
			this.if_special_car=!this.if_special_car;
			if(this.if_special_car)
			{			    
						
				array[0].checked=true;
			}
			else
			{				
				
				array[0].checked=false;
			}
			this.get_length_and_ans();
			
		},
		click_premium_car()
		{
			let that = this;
			let array = getApp().globalData.filter[0].groupContent;
			this.if_premium_car=!this.if_premium_car;
			if(this.if_premium_car)
			{			    
						
				array[1].checked=true;
			}
			else
			{				
				
				array[1].checked=false;
			}
			this.get_length_and_ans();
			
		},
		click_local_licence()
		{
			let license = getApp().globalData.filter[2];
			let that = this;
			let array = getApp().globalData.filter[0].groupContent;
			this.if_local_licence=!this.if_local_licence;
			if(this.if_local_licence)
			{			    					
				array[2].checked=true;
				license.groupContent[0].checked = true;	
			}
			else
			{								
				array[2].checked=false;
				license.groupContent[0].checked = false;	
			}			
			this.get_length_and_ans();
			
		},
		click_unlimited()
		{
			let limited = getApp().globalData.filter[4];
			let that = this;
			let array = getApp().globalData.filter[0].groupContent;
			this.if_unlimited=!this.if_unlimited;
			if(this.if_unlimited)
			{			    						
				array[3].checked=true;
				limited.groupContent[0].checked=true;
			}
			else
			{								
				array[3].checked=false;
				limited.groupContent[0].checked=false;
			}
			this.get_length_and_ans();
				
		},		
		go_to_car_detail()
		{
			uni.navigateTo({
				url:'../car_detail/car_detail'
			})
		},
		toSearchDetails() {
			console.log('搜索框内是:', this.keyword);
			uni.navigateTo({
			    url: '/pages/carList/searchDetails',
			    animationType: 'pop-in',
			    animationDuration: 200
			});
		},
		search_change()
		{
			
		},
		search_search()
		{
			
		},
		choose_place()
		{
			getApp().globalData.is_from_carList = 1;
			uni.navigateTo({
				url:'../city_choice/city_choice'
			})
		}
		
	},
	computed:{		
		isNotActive(){
			return this.list_length===0;
		}
	}
};
</script>

<style scoped lang="scss">
	// 定义弹性容器的样式
.flex{
	display: flex;
	justify-content: space-around; 
	width: 100%;

}
// 四个筛选条件未选中样式
.not_choose_filter {
	background-color: #f6f6f6;
	width: 20%;
	height: 60rpx;
	text-align: center;
	line-height: 60rpx;
	border-radius: 25rpx;
}
// 四个筛选条件选中样式
.is_choose_filter{
	background-color: rgb(255,153,0);
	color: white;
	width: 20%;
	height: 60rpx;
	text-align: center;
	line-height: 60rpx;
	border-radius: 25rpx;
}
.place_and_time{
	width: 30%;
	font-size: 30rpx;
	height: 80rpx;
	line-height: 80rpx;
	margin-bottom: 20rpx;
	text-align: center;
	border-radius: 10rpx;
	border: 1rpx #eaeaea solid;
}
.active {
	background-color: orange;
	color: #fff;
}
.nav-filter {
	margin-bottom: 20rpx;
}

	
.nav-search {
margin-top: 10rpx;
margin-bottom: 20rpx;
}




.fill {
	height: 20rpx;
	background-color: #e0dee1;
}
.notActive{
	background-color: #fff;
	color:#000;
}
</style>
