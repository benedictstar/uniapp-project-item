<template>
	<view class="pages">
		<view class="header">
			123123123123
		</view>
	
		<view class="mainer">
			<u-collapse>
				<u-collapse-item :title="item.head" v-for="(item, index) in itemList" :key="index">
				<view class="content">
					{{item.body}}
				</view>	
				</u-collapse-item>
			</u-collapse>
		</view>
		
		<view class="footer">
			<form action="">
			<input class="input1" type="text"  v-model="formlist[0].username" placeholder="姓名"/>
			<input class="input1" type="text"  v-model="formlist[0].mobile" placeholder="电话"/>
			<input class="input1" type="text"  v-model="formlist[0].car_owned.brand" placeholder="车辆品牌"/>
			<input class="input1" type="text"  v-model="formlist[0].car_owned.type" placeholder="车辆型号"/>
			<input class="input1" type="text"  v-model="formlist[0].car_owned.year_type" placeholder="车辆年限"/>
			<input class="input1" type="text"  v-model="formlist[0].address" placeholder="车主地址"/>
			</form>
			
			
			<button class="btn1" type="default" @click="clickhandle">提交</button>
			
			
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				formlist:[{
					username:"nihao",
					mobile:123,
					address:"北京",
                     car_owned:{
						 brand:"nihao",
						 type:"宝马",
						 year_type:2020,
						 
						 
					 }				
					
				}
					
				],

				
				itemList: [{
					head: "什么是私家车共享",
					body: "私家车共享就是让车主将闲置车辆通过大方共享平台租给他人使用。车主可以依据大方租车的租车标准租给符合条件的租客，并且赚取收益，每月收益可达4500元（15万车型）。",
					open: true,
					disabled: true
				},{
					head: "共享期间如何保障我的车辆安全",
					body: "大方租车使用支付宝信用免押租车，客户信用等级比较高。大方租车拥有专业强大的风控系统，通过网络大数据筛选优质租户。由大方租车遍布全国的线下门店提供管车服务，保障车辆安全。",
					open: false,
				},{
					head: "车辆共享时我需要用车怎么办",
					body: "参与共享的车主，可以随时用车，共两种方案可选：1,提前联系平台预定，将按照约定为您预留车辆。2,临时用车，若爱车已预定或在租，可按照约定有多种车辆供您选择。",
					open: false,
				},{
					head: "私家车共享的收益怎么算",
					body: "车主可选收益模式:分成模式：1.车辆租金收益您和平台按照7:3的效益分成；2.保底收益模式：根据当地租金水平设定保底月租。3.保底收益+分成模式：无论车辆是否出租，保底收益和分成模式取高者。",
					open: false,
				},{
					head: "共享期间车辆的违章怎么处理",
					body: "根据租车合同处理，租赁期间违章由承租人负责处理，门店和平台负责帮助解决。",
					open: false,
				},{
					head: "共享期间车辆怎么保养",
					body: "本合同履行之日起，运营5000公里以上的常规保养相关事宜和费用由我们平台承担。",
					open: false,
				},{
					head: "共享期间车辆损伤，事故，维修怎么处理",
					body: "租赁期间产生的事故、违章、保养、维修，由门店提供服务并负责帮助解决，车主无麻烦。车辆自身原因导致的损伤、事故、维修由车主承担。",
					open: false,
				},
				],
			}
		},
		methods:{
			clickhandle(){
				uni.showToast({
					title:'提交成功',
					duration:2000
				});
			}
		}
	}
</script>



<style>
	.header{
		min-height: 1000rpx;
		width: 100%;
		background-image: linear-gradient(to right, #fa709a ,#fee140);
	}
	
	.mainer{
		margin-top:10rpx;
		background-color:#F5F5F5;
		padding: 0 20rpx;
	}
	.mainer /deep/ .u-collapse-head{
		font-weight: bold;
		border-top: 1rpx dashed #000000;
	}
	.mainer /deep/ .u-collapse-content{
		padding-bottom:15rpx ;
	}
	.content{
		font-size: 12rpx;
	}
	.input1{
		border: 1rpx solid #000000;
		height: 50rpx;
		width: 50%;
		margin: 0 auto;
		border-radius:2%;
		padding: 10rpx;
		margin-bottom: 25rpx;
	}
	.btn1{
		width: 80%;
		background-color: #FF5500;
		color: #FFFFFF;
		margin-bottom: 50rpx;
	}
</style>


