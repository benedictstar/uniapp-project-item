<template>
	<!-- <view class="bottom">
		这是底部组件
	</view> -->
	<view>
		<u-navbar back-icon-color="white" title="确认订单" :background="background" title-color="white" ></u-navbar>
		<view class="head">
			<view class="head1"></view>
		</view>
		<view class="tol">
			<view class="top">
				<view class="common-card">
					<view class="carpage">
						<view class="ima">
							<image :src="imasrc" style="height:180rpx;width:220rpx;border-radius: 30rpx;margin-top:20rpx;margin-left: 25rpx;"></image>
						</view>
						<view style="margin-left:20rpx;margin-top: 40rpx;">
							<view style="margin-top: 10rpx;margin-bottom: 10rpx;">
								<text space="nbsp" style="font-weight: bold;font-size: 36rpx;">保时捷  S型  2021款</text>
							</view>
							<view style="font-size:20rpx;color: #8c8c8c;">
								<view style="margin-top: 10rpx;margin-bottom: 5rpx;">粤A12345</view>
								<view style="margin-top: 5rpx;margin-bottom: 10rpx;">日均限300km</view>
							</view>
						</view>
					</view>
					<!-- <u-gap height="6" bg-color="#f7f7f7" margin-top="30" margin-bottom="30"></u-gap> -->
					<!-- 租还车时间 -->
					<view></view>
					<u-gap height="6" bg-color="#f7f7f7" margin-top="30" margin-bottom="30"></u-gap>
					<!-- 车辆租金 -->
					<view class="carloan">
						<view style="flex-basis: 81%;font-size:25rpx">车辆租金</view>
						<view style="font-size:20rpx">
							<text style="font-weight:light" space="nbsp">¥ {{capital}} × {{days}}天</text>
							<view style="font-size:25rpx;font-weight:bold;margin-left:50rpx">¥ {{capital*days}}</view>
						</view>
					</view>
					<u-gap height="6" bg-color="#f7f7f7" margin-top="30" margin-bottom="30"></u-gap>
					<!-- 平台优惠券 -->
					<view class="dis">
						<!-- <view style="flex-basis: 6%;height:25rpx">
							<image style="height:25rpx;width:25rpx;border-radius: 10rpx;" :src="littleicon"></image>
						</view> -->
						<u-icon name="" label="优惠券" label-size="25" size="25rpx" style="flex-basis: 80%;"></u-icon>
						<!-- <view style="flex-basis: 60%;font-size: 25rpx;">平台优惠券</view> -->
						<!-- <view style="color: red;font-size:25rpx;">-{{discount}}元</view> -->
						<u-icon name="minus"  color="red" size="15rpx" style="flex-basis:4%"></u-icon>
						<u-icon name="rmb" :label="discount" size="20rpx" color="red" label-pos="right" label-color="red" style="flex-basis:12%"></u-icon>
						<u-icon name="arrow-right" label-size="25" size="20rpx"></u-icon>
					</view>
					<!-- <u-cell-group>
						<u-cell-item icon="gift" title="平台优惠券" value="100" style="height:10rpx" label-style="font-size:30rpx">
						</u-cell-item>
					</u-cell-group> -->
				</view>
				<!-- 驾驶员信息界面 -->
				<view class="common-card">
					<view style="display:flex">
						<view style="font-size: 27rpx;font-weight: bolder;margin-top: 2rpx;flex-basis: 75%;">驾驶员信息</view>
						<!-- <u-icon name="question" label="切换驾驶员" label-color="#4690d5" color="#4690d5" size="25" label-size="25" @click="changed"></u-icon> -->
						<u-button hover-class="backgroundColor:#ff5500" @click="changed" shape="circle" size="mini" :hair-line="false" style="font-size: 20rpx;color: #000000;border:1rpx solid rgb(241,201,151);">切换驾驶员</u-button>
					</view>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom="30" margin-top="10"></u-gap>
					 <view class="m-content">
						 <view style="margin-top:10rpx;display:flex;height:40rpx">
							 <!-- <view style="font-size: 25rpx;">驾驶员</view> -->
							 <view style="font-weight: bold;font-size: 28rpx;flex-basis: 18%">{{currentuser.name}}</view>
							 <view style="font-size:25rpx">{{currentuser.tele}}</view>
						 </view>
						 <view style="display:flex;height:40rpx;margin-top:20rpx">
							 <view style="flex-basis: 18%;font-size:25rpx;font-weight: bold;">{{currentuser.cardname}}</view>
							 <view style="flex-basis: 75%;font-size:25rpx">{{currentuser.idcard}}</view>
							 <!-- <view style="height:20rpx">
							 <u-icon name="man-add" size="35rpx"></u-icon>
							 </view> -->
						 </view>
						 <!-- <u-gap height="4" bg-color="#e5e5e5" margin-bottom="30"></u-gap>
						 <view style="font-size:25rpx">联系电话</view>
						 <view style="display:flex;height:40rpx;margin-top:20rpx">
							<view style="flex-basis: 93%;font-size:25rpx">{{currentuser.tele}}</view>
							<view style="height:20rpx">
							<u-icon name="coupon" size="35rpx"></u-icon>
							</view>
						 </view>
						 <u-gap height="4" bg-color="#e5e5e5" margin-bottom="20"></u-gap> -->
					 </view>
				</view>
				<view class="common-card">
					<view class="title">押金支付方式</view>
					<u-gap height="4" bg-color="#e5e5e5" margin-top="10"></u-gap>
					<view class="m-content">
						<u-radio-group v-model="pay" style="width: 100%;">
							<u-radio name="xianshang" active-color="#ff5500" style="border: 4rpx solid rgb(241,201,151);width:100%;padding-left: 30rpx;margin-top: 30rpx;border-radius: 30rpx;">
									<view class="box-head">线上支付押金</view>
									<view class="box-content">
										<!-- <text>
											在线支付押金，取车时通过信用卡进行车辆押金预授权
										</text> -->
										<view>在线支付押金,</view>
										<view>取车时通过信用卡进行车辆押金预授权</view>
									</view>
							</u-radio>
							<!-- #ifndef MP-WEIXIN -->
							<u-radio class="radio" active-color="#ff5500" name="zhima" style="border: 4rpx solid rgb(241,201,151);width:100%;padding-left: 30rpx;margin-top: 30rpx;border-radius: 30rpx">
									<view class="box-head">芝麻信用免押金</view>
									<view class="box-content">
										<!-- <text style="word-break: break-all;"> -->
										<view>芝麻分550分及以上,</view>
										<view>有机会享受30000元租车押金双免服务</view>
										<!-- </text> -->
									</view>
							</u-radio>
							<!-- #endif -->
							<u-radio name="xianxia"  active-color="#ff5500" style="border: 4rpx solid rgb(241,201,151);width:100%;padding-left: 30rpx;margin-top: 30rpx;border-radius: 30rpx">
								
									<view class="box-head">线下支付押金</view>
									<view class="box-content">
										<!-- <text>
											押金到店支付，线下先交押金再提车
										</text> -->
										<view>押金到店支付,</view>
										<view>线下先交押金再提车</view>
									</view>
								
							</u-radio>
						</u-radio-group>
					</view>
				</view>
				<view class="common-card">
					<view>
						<u-tabs  font-size="20rpx" duration=0.2 :list="noticelist" active-color="#ff5500" :current="tabIndex" @change="change"></u-tabs>
					</view>
					<swiper class="swiper-box" :style="{height:swiperheight+'px'}" :current="tabIndex" @change="tabChange">
						<swiper-item v-for="(items,index) in newslist" :key="index">
							<view style="word-break: break-all;word-wrap: break-word;white-space: pre-line;">{{items.content}}</view>
						</swiper-item>
					</swiper>
				</view>
			</view>
			<u-popup v-model="show" mode="bottom" border-radius="20" height="42%">
				<view style="margin-top: 20rpx;margin-left: 40rpx;">
					<view style="display:flex;margin-top:30rpx">
						<view style="flex-basis: 89%;font-size:30rpx;font-weight: bold;">基础服务费</view>
						<view style="font-size:20rpx">
							<!-- <text style="font-size:25rpx;font-weight:bold;margin-left:20rpx">{{server}}元</text> -->
							<u-icon name="rmb" label-pos="right" :label="capital*days"></u-icon>
						</view>
					</view>
					<view style="font-size:20rpx;display: flex;">
						<view style="flex-basis: 83%;"></view>
						<text style="font-weight:light" space="nbsp">{{capital}} ¥ × {{days}}天</text>
					</view>
					<view style="display:flex;margin-top:30rpx">
						<view style="flex-basis: 89%;font-size:30rpx;font-weight: bold;">基础服务费</view>
						<view style="font-size:20rpx">
							<!-- <text style="font-size:25rpx;font-weight:bold;margin-left:20rpx">{{server}}元</text> -->
							<u-icon name="rmb" label-pos="right" :label="server"></u-icon>
						</view>
					</view>
					<view style="display:flex;margin-top:30rpx">
						<view style="flex-basis: 89%;font-size:30rpx;font-weight: bold;">车行手续费</view>
						<view style="font-size:20rpx">
							<!-- <text style="font-size:25rpx;font-weight:bold;margin-left:20rpx">{{server}}元</text> -->
							<u-icon name="rmb" label-pos="right" :label="charge"></u-icon>
						</view>
					</view>
					<view style="font-weight: light;font-size:23rpx">用于车辆清洁、车辆保养、单据制作、人员服务等</view>
					<view style="display:flex;margin-top:30rpx">
						<view style="flex-basis: 81%;font-size:30rpx;font-weight: bold;">全额</view>
						<view style="font-size:20rpx">
							<!-- <text style="font-size:25rpx;font-weight:bold;margin-left:20rpx">{{server}}元</text> -->
							<u-icon name="rmb" label-pos="right" :label="charge+capital*days+server" size="40" label-color="#ff5500"
							label-size="40" color="#ff5500" ></u-icon>
						</view>
					</view>
					<view style="margin-left:82%;font-size:26rpx;margin-top: 25rpx;">在线支付</view>
				</view>
			</u-popup>
			<!-- 底部总高度130rpx -->
			<!-- <view :class="[checked===0?'noc2':'noc']">
				<u-radio-group v-model="value">
					<u-radio name="protocol" active-color="#ff5500" label-size="25rpx" icon-size="30rpx" class="nc" @change="radiochange">我已阅读并同意《来往租车协议》</u-radio>
				</u-radio-group>
				<radio-group >
					<label v-for="(item, index) in List" :key="index" @click="radioChange(index)" >
						<view  class="nc">
						<radio style="transform:scale(0.7)" color="#ff5500" :class="active == index ? 'checked' : ''" :checked="active== index"  />
						{{item.lb}}
						</view>
					</label>
				</radio-group>
			</view> -->
			<view class="bottom">
				<view class="bottom1">
					<view style="margin-top: 10rpx;">
						<radio-group >
							<label style="display: flex;marign-top:10rpx;margin-left: 30rpx;" v-for="(item, index) in List" :key="index" @click="radioChange(index)" >
								<view style="width:40rpx;">
									<radio style="transform:scale(0.5)" color="#ff5500" :class="active == index ? 'checked' : ''" :checked="active== index"  />
								</view>
								<view style="margin-top: 7rpx;font-size: 20rpx;">
									{{item.lb}}
								</view>
							</label>
						</radio-group>
					</view>
					<view class="bo1">
						<view style="display: flex;">
							<view style="flex-basis: 40%;margin-top: 4rpx;" >
								<text>订单租金:</text>
								<text style="color:#ff5500;margin-left:20rpx" space="nbsp">¥{{money}}</text>
							</view>
							<view>
								<u-icon name="arrow-right" label="费用明细" label-color="#ff5500"
								color="#ff5500" label-pos="left" label-size="20" size="15"
								@click="fare"></u-icon>
								</view>
							</view>
							<view style="color:#ff5500">
								<text>已减{{discount}}元</text>
							</view>
						</view>
				</view>
				<!-- <view style="margin-top:10rpx;">
					<u-icon name="arrow-right" label="费用明细" label-color="#ff5500"
					color="#ff5500" label-pos="left" label-size="20" size="15"
					@click="show=true"></u-icon>
					</view>
				</view> -->
				<view>
						<button  class="bu">确认支付</button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return{
				List:[
					{lb:'我已阅读并同意《来往租车协议》'}
				],
				charge:40,
				server:80,
				show:false,
				discount:108,
				money:10,
				checked:0,//checked值为0则未选中，为1则选中
				value:'',
				active: null,
				pay:'xianshang',
				currentuser:'',
				littleicon:'/static/1.jfif',
				// discount:100,
				capital:10,
				days:2,
				imasrc:'/static/1.jfif',
				src:'/static/1.jfif',
				noticelist:[
					{name:'取车必备证件'},
					{name:'押金预授权'},
					{name:'取消订单违约金'},
					{name:'燃油说明和里程限制'},
					{name:'发票说明'},
					{name:'限制出行区域'},
					{name:'更多规则'}
				],
				tabIndex:0,
				swiperheight:200,
				newslist:[
					{content:'A'},
					{content:'B'},
					{content:'C'},
					{content:'D'},
					{content:'E'},
					{content:'F'},
					{content:'G'},
				],
				background:{
					backgroundColor: '#ff5500',
				},
			}
		},
	  //   components: {
			// bottom1,
			// bottom2
			// },
		onShow()
		{
			
		},
		methods:{
			onLoad(){
			// 	this.currentuser=getApp().globalData.driverinf[getApp().globalData.driverinf_index]
			},
			onShow()
			{
				this.currentuser=getApp().globalData.driverinf[getApp().globalData.driverinf_index]
			},
			fare(){
				uni. navigateTo({
					url:'./fare'
				})
			},
			change(index){
				this.tabIndex = index;
			},
			tabChange(e){
			   this.tabIndex = e.detail.current;
			},
			changed(){
				uni. navigateTo({
					url:'./changedriver'
				})
			},
			radioChange(index) {
			    if (this.active== index) { // 如果已经选中，则取消选中
			        this.active= null;
					this.checked=0;
			    } else { // 否则进行选中赋值
			        this.active= index;
					this.checked=1;
			    }
			}
		},
	}
	
</script>

<style>
	/* .bottom{
	height:100rpx;
	width:100%;
	bottom:0rpx;
	position:fixed;
	background-color:white;
	} */
	page{
		background-color: #ebebeb;
	}
	.hclass{
		color: $u-type-primary-dark !important;
		background: $u-type-primary-light !important;
	}
	.head{
		height: 50rpx;
		width: 100%;
		top:44;
		background-color: #ff5500;
		position: fixed;
		
	}
	.head1{
		height: 50rpx;
		background-color:#ebebeb;
		opacity: 0.97;
		border-radius: 100rpx 100rpx 0 0;
		z-index: -1;
	}
	.tol{
		border-radius: 40rpx 40rpx 0 0;
		background-color: #ebebeb;
	}
	.top{
		display:flex;
		flex-direction: column;
		margin-bottom: 70rpx;
	}
	.carpage{
		display:flex;
	}
	.carpage .ima{
		/* height:40rpx;
		width:40rpx; */
		/* height:10rpx; */
	}
	.carloan{
		display:flex;
	}
	.dis{
		display:flex;
		flex:1;
		border:none;
	}
	.common-card {
			background-color: #fff;
			padding: 20rpx;
			margin-top: 35rpx;
			margin-left: 33rpx;
			margin-right: 33rpx;
			border-radius: 30rpx;
			box-shadow: 5rpx 8rpx 15rpx #c8c8c8;
			position: relative;
			z-index: 1;
			
			
		}
	.common-card .title{
			font-size: 27rpx;
			font-weight: bolder;
			margin-top: 2rpx;
		}
	.common-card .m-content{
		/* display:flex;
		flex-direction: column; */
	}
	.common-card .m-content .box-head{
		font-size:26rpx;
		font-weight: bold;
		margin-top:20rpx;
		margin-left:20rpx;
		margin-bottom: 10rpx;
		width:100%
	}
	.common-card .m-content .box-content{
		font-size:20rpx;
		margin-left:20rpx;
		margin-bottom:20rpx;
		margin-top:10rpx;
		color:#585858;
		word-break: break-all;
		word-wrap: break-word;
		white-space: pre-line;
		width:100%
		
	}
	.bottom{
	display:flex;
	height:130rpx;
	width:90%;
	bottom:20rpx;
	position:fixed;
	z-index: 9999;
	background-color:rgb(241,201,151);
	font-size:18rpx;
	margin-left: 5%;
	margin-right: 5%;
	border-radius: 65rpx;
	}
	.bottom1{
	display:flex;
	flex-direction: column;
	font-size:18rpx;
	flex-basis: 70%;
	}
	.bu{
		background-color: #ff5500;
		color:white;
		height:70rpx;
		width:180rpx;
		text-align: center;
		font-size:28rpx;
		border-radius: 40rpx;
		margin-top: 30rpx;
		margin-bottom: 30rpx;
		
	}
	.bo1{
		margin-top:10rpx;
		margin-bottom: 10rpx;
		margin-left:70rpx;
		font-size:20rpx;
		width:100%
	}
	/* .noc{
		display:flex;
		bottom: 85rpx;
		position:fixed;
		background-color: #f3f300;
		width: 100%;
		height:50rpx;
		font-size: 20rpx;
	}
	.noc2{
		display:flex;
		bottom: 85rpx;
		position:fixed;
		background-color: #FFFFFF;
		width: 100%;
		height:50rpx;
		font-size: 20rpx;
	} */
	.nc{
		margin-left:30rpx;
		margin-top:5rpx;
		font-size: 20rpx;
		
	}
	
</style>
