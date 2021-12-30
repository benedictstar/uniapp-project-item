<!-- 订单页面 -->
<template>
	<view>
		<view class="" style="height: 100rpx; background-color: #e35c31;">
		</view>
		<view class="wrap" style="position: relative; top: -70rpx; border-top-left-radius: 35rpx;border-top-right-radius: 35rpx">
			<view class="u-tabs-box" style="margin-top: 15rpx; display: flex; justify-content: space-around;">
				<!-- <u-tabs-swiper
					activeColor="#f29100"
					ref="tabs"
					:list="navTabList"
					:current="navTabCurrent"
					@change="navTabChange"
					:is-scroll="false"
					swiperWidth="750"
				></u-tabs-swiper> -->
				<view class="top_title" @click="navTabChange(0)" :class="{'choose':swiperCurrent==0,'not_choose':swiperCurrent!=0}">
					全部
				</view>
				<view class="top_title" @click="navTabChange(1)"  :class="{'choose':swiperCurrent==1,'not_choose':swiperCurrent!=1}">
					进行中
				</view>
				<view class="top_title" @click="navTabChange(2)"  :class="{'choose':swiperCurrent==2,'not_choose':swiperCurrent!=2}">
					已完成
				</view>
				<view class="top_title" @click="navTabChange(3)"  :class="{'choose':swiperCurrent==3,'not_choose':swiperCurrent!=3}">
					已取消
				</view>
			</view>
			

			<swiper class="swiper-box" :current="swiperCurrent">

			<!--全部-->
			<swiper-item class="swiper-item">
				<scroll-view scroll-y style="height: 100%;width: 100%;" @scrolltolower="reachBottom">
					<view class="page-box">
						<!-- 所有订单 -->
						<view class="order"  v-for="(res, index) in orderList[0]" style="display: flex; justify-content: space-between;">
							<!-- 左边页面 -->
							<view class="" style="width: 92%; ">
								<!-- 下单时间 -->
								<view class="" @click="go_to_order_list">
									<view class="">
										<view class="" style="margin-top: 10rpx; font-size: smaller; color: #F2F2F2;">下单时间：{{ res.order_time }}</view>
									</view>									
								</view>
								<!-- 内容 -->
								<view class="item" @click="go_to_order_list" v-for="(item, index) in res.goodsList" :key="index">
									<!-- 左边图片 -->
									<view class="left"><image :src="item.goodsUrl" mode="aspectFill"></image></view>
									<!-- 车名,地址和时间 -->
									<view class="content">
										<view class="keywords">{{res.keywords }}</view>
										<view class="type">{{ item.start }}至{{ item.end }}</view>
										<view class="title">{{ item.addr }}</view>
									</view>
								</view>
								<!-- 共多少天，合计 -->
								<view class="total" @click="go_to_order_list" style="padding-bottom: 20rpx; border-bottom: 1rpx rgb(227, 227, 227) solid ;">
									共{{ totalNum(res.goodsList) }}天次 合计:
									<text class="total-price">
										￥{{ priceInt(totalPrice(res.goodsList)) }}.
										<text class="decimal">{{ priceDecimal(totalPrice(res.goodsList)) }}</text>
									</text>
								</view>
								<!-- 三个按钮 -->
								<view v-if="res.deal === '待付款'" class="bottom">
									<view class="more"><u-icon name="more-dot-fill" color="rgb(203,203,203)"></u-icon></view>
									<view class="logistics btn">联系车管家</view>
									<view class="exchange btn">联系车主</view>
									<view class="evaluate btn"@click="go_to_order_list">立即支付</view>
								</view>
								<!-- 三个按钮 -->
								<view v-else class="bottom">
									<view class="more"><u-icon name="more-dot-fill" color="rgb(203,203,203)"></u-icon></view>
									<view class="evaluate btn" @click="go_to_order_list">再次预定</view>
								</view>
							</view>
							<!-- 右边按钮 -->
							<view class="" @click="go_to_order_list" style="width: 8%;  color: white; text-align: center; background-color: #e35c31; border-bottom-right-radius: 20rpx; border-top-right-radius: 20rpx;">
								<view class="right" style="margin-top: 140rpx;">{{ res.deal }}</view>
							</view>
						</view>
						<!-- 加载更多 -->
						<u-loadmore :status="loadStatus[0]" bgColor="#f2f2f2"></u-loadmore>
					</view>
				</scroll-view>
			</swiper-item>
			<!--进行中-->
			<swiper-item class="swiper-item">
				<scroll-view scroll-y style="height: 100%;width: 100%;" @scrolltolower="reachBottom">
					<view class="page-box">
						<!-- 所有订单 -->
						<view class="order"  v-for="(res, index) in orderList[1]" style="display: flex; justify-content: space-between;">
							<!-- 左边页面 -->
							<view class="" style="width: 92%; ">
								<!-- 下单时间 -->
								<view class="" @click="go_to_order_list">
									<view class="">
										<view class="" style="margin-top: 10rpx; font-size: smaller; color: #F2F2F2;">下单时间：{{ res.order_time }}</view>
									</view>									
								</view>
								<!-- 内容 -->
								<view class="item" @click="go_to_order_list" v-for="(item, index) in res.goodsList" :key="index">
									<!-- 左边图片 -->
									<view class="left"><image :src="item.goodsUrl" mode="aspectFill"></image></view>
									<!-- 车名,地址和时间 -->
									<view class="content">
										<view class="keywords">{{res.keywords }}</view>
										<view class="type">{{ item.start }}至{{ item.end }}</view>
										<view class="title">{{ item.addr }}</view>
									</view>
								</view>
								<!-- 共多少天，合计 -->
								<view class="total" @click="go_to_order_list" style="padding-bottom: 20rpx; border-bottom: 1rpx rgb(227, 227, 227) solid ;">
									共{{ totalNum(res.goodsList) }}天次 合计:
									<text class="total-price">
										￥{{ priceInt(totalPrice(res.goodsList)) }}.
										<text class="decimal">{{ priceDecimal(totalPrice(res.goodsList)) }}</text>
									</text>
								</view>
								<!-- 三个按钮 -->
								<view v-if="res.deal === '待付款'" class="bottom">
									<view class="more"><u-icon name="more-dot-fill" color="rgb(203,203,203)"></u-icon></view>
									<view class="logistics btn">联系车管家</view>
									<view class="exchange btn">联系车主</view>
									<view class="evaluate btn"@click="go_to_order_list">立即支付</view>
								</view>
								<!-- 三个按钮 -->
								<view v-else class="bottom">
									<view class="more"><u-icon name="more-dot-fill" color="rgb(203,203,203)"></u-icon></view>
									<view class="evaluate btn" @click="go_to_order_list">再次预定</view>
								</view>
							</view>
							<!-- 右边按钮 -->
							<view class="" style="width: 8%;  color: white; text-align: center; background-color: #e35c31; border-bottom-right-radius: 20rpx; border-top-right-radius: 20rpx;">
								<view class="right" style="margin-top: 140rpx;">{{ res.deal }}</view>
							</view>
						</view>
						<!-- 加载更多 -->
						<u-loadmore :status="loadStatus[0]" bgColor="#f2f2f2"></u-loadmore>
					</view>
				</scroll-view>
			</swiper-item>
			<!--已完成-->
			 <swiper-item class="swiper-item">
			 	<scroll-view scroll-y style="height: 100%;width: 100%;" @scrolltolower="reachBottom">
			 		<view class="page-box">
			 			<!-- 所有订单 -->
			 			<view class="order"  v-for="(res, index) in orderList[2]" style="display: flex; justify-content: space-between;">
			 				<!-- 左边页面 -->
			 				<view class="" style="width: 92%; ">
			 					<!-- 下单时间 -->
			 					<view class="" @click="go_to_order_list">
			 						<view class="">
			 							<view class="" style="margin-top: 10rpx; font-size: smaller; color: #F2F2F2;">下单时间：{{ res.order_time }}</view>
			 						</view>									
			 					</view>
			 					<!-- 内容 -->
			 					<view class="item" @click="go_to_order_list" v-for="(item, index) in res.goodsList" :key="index">
			 						<!-- 左边图片 -->
			 						<view class="left"><image :src="item.goodsUrl" mode="aspectFill"></image></view>
			 						<!-- 车名,地址和时间 -->
			 						<view class="content">
			 							<view class="keywords">{{res.keywords }}</view>
			 							<view class="type">{{ item.start }}至{{ item.end }}</view>
			 							<view class="title">{{ item.addr }}</view>
			 						</view>
			 					</view>
			 					<!-- 共多少天，合计 -->
			 					<view class="total" @click="go_to_order_list" style="padding-bottom: 20rpx; border-bottom: 1rpx rgb(227, 227, 227) solid ;">
			 						共{{ totalNum(res.goodsList) }}天次 合计:
			 						<text class="total-price">
			 							￥{{ priceInt(totalPrice(res.goodsList)) }}.
			 							<text class="decimal">{{ priceDecimal(totalPrice(res.goodsList)) }}</text>
			 						</text>
			 					</view>
			 					<!-- 三个按钮 -->
			 					<view v-if="res.deal === '待付款'" class="bottom">
			 						<view class="more"><u-icon name="more-dot-fill" color="rgb(203,203,203)"></u-icon></view>
			 						<view class="logistics btn">联系车管家</view>
			 						<view class="exchange btn">联系车主</view>
			 						<view class="evaluate btn"@click="go_to_order_list">立即支付</view>
			 					</view>
			 					<!-- 三个按钮 -->
			 					<view v-else class="bottom">
			 						<view class="more"><u-icon name="more-dot-fill" color="rgb(203,203,203)"></u-icon></view>
			 						<view class="evaluate btn" @click="go_to_order_list">再次预定</view>
			 					</view>
			 				</view>
			 				<!-- 右边按钮 -->
			 				<view class="" style="width: 8%;  color: white; text-align: center; background-color: #e35c31; border-bottom-right-radius: 20rpx; border-top-right-radius: 20rpx;">
			 					<view class="right" style="margin-top: 140rpx;">{{ res.deal }}</view>
			 				</view>
			 			</view>
			 			<!-- 加载更多 -->
			 			<u-loadmore :status="loadStatus[0]" bgColor="#f2f2f2"></u-loadmore>
			 		</view>
			 	</scroll-view>
			 </swiper-item>
			 
			<!--已取消-->
			 <swiper-item class="swiper-item">
			 	<scroll-view scroll-y style="height: 100%;width: 100%;" @scrolltolower="reachBottom">
			 		<view class="page-box">
			 			<!-- 所有订单 -->
			 			<view class="order"  v-for="(res, index) in orderList[3]" style="display: flex; justify-content: space-between;">
			 				<!-- 左边页面 -->
			 				<view class="" style="width: 92%; ">
			 					<!-- 下单时间 -->
			 					<view class="" @click="go_to_order_list">
			 						<view class="">
			 							<view class="" style="margin-top: 10rpx; font-size: smaller; color: #F2F2F2;">下单时间：{{ res.order_time }}</view>
			 						</view>									
			 					</view>
			 					<!-- 内容 -->
			 					<view class="item" @click="go_to_order_list" v-for="(item, index) in res.goodsList" :key="index">
			 						<!-- 左边图片 -->
			 						<view class="left"><image :src="item.goodsUrl" mode="aspectFill"></image></view>
			 						<!-- 车名,地址和时间 -->
			 						<view class="content">
			 							<view class="keywords">{{res.keywords }}</view>
			 							<view class="type">{{ item.start }}至{{ item.end }}</view>
			 							<view class="title">{{ item.addr }}</view>
			 						</view>
			 					</view>
			 					<!-- 共多少天，合计 -->
			 					<view class="total" @click="go_to_order_list" style="padding-bottom: 20rpx; border-bottom: 1rpx rgb(227, 227, 227) solid ;">
			 						共{{ totalNum(res.goodsList) }}天次 合计:
			 						<text class="total-price">
			 							￥{{ priceInt(totalPrice(res.goodsList)) }}.
			 							<text class="decimal">{{ priceDecimal(totalPrice(res.goodsList)) }}</text>
			 						</text>
			 					</view>
			 					<!-- 三个按钮 -->
			 					<view v-if="res.deal === '待付款'" class="bottom">
			 						<view class="more"><u-icon name="more-dot-fill" color="rgb(203,203,203)"></u-icon></view>
			 						<view class="logistics btn">联系车管家</view>
			 						<view class="exchange btn">联系车主</view>
			 						<view class="evaluate btn"@click="go_to_order_list">立即支付</view>
			 					</view>
			 					<!-- 三个按钮 -->
			 					<view v-else class="bottom">
			 						<view class="more"><u-icon name="more-dot-fill" color="rgb(203,203,203)"></u-icon></view>
			 						<view class="evaluate btn" @click="go_to_order_list">再次预定</view>
			 					</view>
			 				</view>
			 				<!-- 右边按钮 -->
			 				<view class="" style="width: 8%;  color: white; text-align: center; background-color: #e35c31; border-bottom-right-radius: 20rpx; border-top-right-radius: 20rpx;">
			 					<view class="right" style="margin-top: 140rpx;">{{ res.deal }}</view>
			 				</view>
			 			</view>
			 			<!-- 加载更多 -->
			 			<u-loadmore :status="loadStatus[0]" bgColor="#f2f2f2"></u-loadmore>
			 		</view>
			 	</scroll-view>
			 </swiper-item>
		</swiper>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			orderList: [[], [], [], []],
			dataList: [
				{
					id: 111,
					keywords: '法拉利 F12 berlinetta 6.3L',
					order_time:'2021/7/1',
					deal: '已完成',

					goodsList: [
						{
							goodsUrl: 'https://carphoto.atzuche.com/car/21/06/979162126/1624199630427_1.jpg',
							price: '1348.58',
							number: 2,
							start: '2021/7/8 ',
							end: '2021/7/10 ',
							addr: '广州市番禺区小谷围街道华南理工大学'
						}
					]
				},
				{
					id: 222,
					keywords: '奔驰S级(进口) 3.0T',
					order_time:'2021/7/1',
					deal: '待付款',
					goodsList: [
						{
							goodsUrl: 'https://carphoto.atzuche.com/car/20/06/799509327/1592978935791_1.jpg',
							price: '1598',
							number: 2,
							start: '2021/7/8 ',
							end: '2021/7/10 ',
							addr: '广州市番禺区小谷围街道华南理工大学'
						}
					]
				},
				{
					id: 333,
					keywords: '奔驰SLS级AMG(进口) 6.2L',
					order_time:'2021/7/1',
					deal: '待付款',
					goodsList: [
						{
							goodsUrl: 'https://carphoto.atzuche.com/car/21/06/629856728/1624198858127_1.jpg',
							price: '1950',
							number: 3,
							start: '2021/7/9',
							end: '2021/7/12',
							addr: '广州市番禺区小谷围街道华南理工大学'
						}
					]
				},
				{
					id: 444,
					keywords: '兰博基尼Urus 4.0T',
					order_time:'2021/7/1',
					deal: '已取消',
					goodsList: [
						{
							goodsUrl: 'https://carphoto.atzuche.com/car/21/05/799115425/1623307725750_2.jpg',
							price: '4350',
							number: 3,
							start: '2021/7/8 ',
							end: '2021/7/11 ',
							addr: '广州市番禺区小谷围街道华南理工大学'
						}
					]
				},
				{
					id: 555,
					keywords: '讴歌NSX 3.5T',
					order_time:'2021/7/1',
					deal: '已完成',
					goodsList: [
						{
							goodsUrl: 'https://carphoto.atzuche.com/car/20/12/533286117/1609743169374_1.jpg',
							price: '451',
							number: 9,
							start: '2021/7/8 12:00',
							end: '2021/7/8 14:00',
							addr: '广州市番禺区小谷围街道华南理工大学'
						}
					]
				}
			],
			navTabList: [
				//navTab标签数组，元素为对象
				{
					name: '全部'
				},
				{
					name: '进行中'
				},
				{
					name: '已完成'
				},
				{
					name: '已取消'
					// count: 12
				}
			],
			navTabCurrent: 0, //指定哪个navTab为激活状态
			swiperCurrent: 0,
			tabsHeight: 0,
			dx: 0,
			loadStatus: ['loadmore', 'loadmore', 'loadmore', 'loadmore']
		};
	},
	onLoad() {
		this.getOrderList();
	},
	computed: {
		// 价格小数
		priceDecimal() {
			return val => {
				if (val !== parseInt(val)) return val.slice(-2);
				else return '00';
			};
		},
		// 价格整数
		priceInt() {
			return val => {
				if (val !== parseInt(val)) return val.split('.')[0];
				else return val;
			};
		}
	},
	methods: {
		reachBottom() {
		// 	// 此tab为空数据
		// 	this.loadStatus.splice(this.navTabCurrent, 1, 'loading');
		// 	setTimeout(() => {
		// 		this.getOrderList(this.navTabCurrent);
		// 	}, 1200);
		},

		// 页面数据
		getOrderList() {
			for (const item of this.dataList) {
				this.orderList[0].push(item);
				if (item.deal === '待付款' || item.deal === '进行中') {
					this.orderList[1].push(item);
				} else if (item.deal === '已完成') {
					this.orderList[2].push(item);
				} else if (item.deal === '已取消') {
					this.orderList[3].push(item);
				}
			}
		},
		// getOrderList(idx) {
		// 	for (let i = 0; i < 5; i++) {
		// 		let index = this.$u.random(0, this.dataList.length - 1);
		// 		let data = JSON.parse(JSON.stringify(this.dataList[index]));
		// 		data.id = this.$u.guid();
		// 		this.orderList[idx].push(data);
		// 	}
		// 	this.loadStatus.splice(this.navTabCurrent, 1, 'loadmore');
		// },
		// 总价
		totalPrice(item) {
			let price = 0;
			item.map(val => {
				price += parseFloat(val.price) * val.number;
			});
			return price.toFixed(2);
		},
		// 总天数
		totalNum(item) {
			let num = 0;
			item.map(val => {
				num += val.number;
			});
			return num;
		},
		// tab栏切换
		navTabChange(index) {
			this.swiperCurrent = index;
			this.getOrderList(index);
		},
		// animationfinish({ detail: { current } }) {
		// 	this.$refs.tabs.setFinishCurrent(current);
		// 	this.swiperCurrent = current;
		// 	this.navTabCurrent = current;
		// },
		go_to_order_list()
		{
			uni.navigateTo({
				url:'../details/details'
			})
		}
	}
};
</script>

<style>
/* #ifndef H5 */
page {
	height: 100%;
	background-color: #f2f2f2;
}
/* #endif */
</style>

<style lang="scss" scoped>
.top_title{
	 width: 20%;
	 height: 60rpx;
	 line-height: 60rpx;
	 text-align: center;
	 border-radius: 30rpx;
}
.choose{
	color: white;
	border: 1rpx #E35C31 solid;
	background-color:#E35C31;
}
.not_choose{
	color: #E35C31;
	border: 1rpx #E35C31 solid;
	background-color:#f2f2f2;
}
.keywords {	
	font-size: 32rpx;
	font-weight: bold;
}
.order {
	width: 710rpx;
	background-color: #ffffff;
	margin: 20rpx auto;
	border-radius: 20rpx;
	box-sizing: border-box;
	padding-left: 20rpx;
	font-size: 28rpx;
	.item {
		display: flex;
		margin: 20rpx 0 0;
		.left {
			margin-right: 20rpx;
			image {
				width: 200rpx;
				height: 200rpx;
				border-radius: 10rpx;
			}
		}
		.content {
			.addr {
				font-size: 28rpx;
				line-height: 50rpx;
			}
			
			.end {
				color: #ffcc00;
				font-size: 28rpx;
			}
		}
		.right {
			margin-left: 10rpx;
			padding-top: 20rpx;
			text-align: right;
			.decimal {
				font-size: 24rpx;
				margin-top: 4rpx;
			}
			.number {
				color: $u-tips-color;
				font-size: 24rpx;
			}
		}
	}
	.total {
		margin-right: 10rpx;
		text-align: right;
		font-size: 24rpx;
		.total-price {
			font-size: 28rpx;
		}
	}
	.bottom {
		display: flex;
		margin-top: 10rpx;
		margin-bottom: 10rpx;
		padding: 0 10rpx;
		justify-content: space-between;
		align-items: center;
		.btn {
			line-height: 52rpx;
			width: 160rpx;
			border-radius: 26rpx;
			border: 2rpx solid $u-border-color;
			font-size: 26rpx;
			text-align: center;
			color: $u-type-info-dark;
		}
		.evaluate {
			color: $u-type-warning-dark;
			border-color: $u-type-warning-dark;
		}
	}
}
.type {
	margin: 10rpx 0;
	font-size: smaller;
	color: #ffcc00;
}
.centre {
	text-align: center;
	margin: 200rpx auto;
	font-size: 32rpx;
	image {
		width: 164rpx;
		height: 164rpx;
		border-radius: 50%;
		margin-bottom: 20rpx;
	}
	.tips {
		font-size: 24rpx;
		color: #999999;
		margin-top: 20rpx;
	}
	.btn {
		margin: 80rpx auto;
		width: 200rpx;
		border-radius: 32rpx;
		line-height: 64rpx;
		color: #ffffff;
		font-size: 26rpx;
		background: linear-gradient(270deg, rgba(249, 116, 90, 1) 0%, rgba(255, 158, 1, 1) 100%);
	}
}
.wrap {
	display: flex;
	flex-direction: column;
	height: calc(100vh - var(--window-top));
	width: 100%;
	background-color:#f2f2f2 ;
}
.swiper-box {
	flex: 1;
}
.swiper-item {
	height: 100%;
}
</style>
