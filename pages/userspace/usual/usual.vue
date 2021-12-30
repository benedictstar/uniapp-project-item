<!-- 常用联系人 -->
<template>
	<view>
		<u-navbar title="常用联系人"></u-navbar>
		<view class="main" v-if="have">
			<image :src="src" style="width:200rpx;height:200rpx;"></image>
			<view class="mid">请添加常用驾驶人信息</view>
			<view class="tip">{{ben}}</view>
		</view>
		<view v-else="have">
			<view style="margin-left: 30rpx;margin-right: 30rpx;margin-top: 10rpx;color:#909090;
			font-size:25rpx">{{ben}}</view>
			<u-cell-group>
				<u-cell-item v-for="(item,index) in usual" :key="index" :title="item.name" :value="item.tele" :index="index" @click="people"></u-cell-item>
			</u-cell-group>
		</view>
		<view class="bottom">
			<button class="ur" @click="adduser">添加常用驾驶人</button>
		</view>
		<u-popup mode="bottom" :height="wheight" :closeable="true" v-model="show" close-icon-pos="top-left" :mask="false">
			<view style="font-weight: bold;margin-top:100rpx;font-size:40rpx;margin-left:25rpx">添加常用驾驶人</view>
			<view style="margin:40rpx;">
				<u-form ref="uForm" :model="form">
					<u-form-item label-width="120" label="真实姓名"><u-input :clearable="false" placeholder=" " v-model="form.name" input-align="right"/></u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
					<u-form-item label="手机号">
						<u-input :clearable="false" placeholder=" " v-model="form.tele" maxlength="11" input-align="right"/>
					</u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
					<u-form-item label="身份证">
						<u-input :clearable="false" placeholder=" " v-model="form.idcard" input-align="right"/>
					</u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
					<u-form-item :clearable="false" label="准驾车型" label-width="120">
						<u-input :select-open="show1" :disabled="true" :clearable="false" placeholder=" " v-model="form.type" input-align="right" @click="car"/>
					</u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
					<u-form-item label="驾驶证有效起始日期" label-width="270">
						<u-input :select-open="show2" type="select" :disabled="true" :clearable="false" placeholder=" " v-model="form.date1" input-align="right" @click="begin"/>
					</u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
					<u-form-item label="驾驶证有效终止日期" label-width="270">
						<u-input :select-open="show3" type="select" :disabled="true" :clearable="false" placeholder=" " v-model="form.date2" input-align="right" @click="end"/>
					</u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
				</u-form>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;margin-top:80rpx;margin-left: 40rpx;margin-right: 40rpx;">
				<button class="bu" @click="complete">完成</button>
			</view>
		</u-popup>
		<u-popup mode="bottom" height="650" v-model="show1" :closeable="true" close-icon-pos="top-left">
			<!-- #ifdef MP -->
			<view style="text-align: center;margin-top: 45rpx;font-size: 25rpx;font-weight: bold;">选择准驾车型（可多选）</view>
			<!-- #endif -->
			<!-- #ifndef MP -->
			<view style="text-align: center;margin-top: 30rpx;font-size: 25rpx;font-weight: bold;">选择准驾车型（可多选）</view>
			<!-- #endif -->
			<view style="display:flex;flex-direction: row;margin-left: 30rpx;margin-right: 30rpx;margin-top:70rpx">
				<view v-if="index<=3" v-for="(item,index) in cartype" @click="carty(index)" style="flex-basis: 25%;display: flex;flex-direction: column;align-items: center;height:70rpx;">
					<view :class="[cartype[index].confirmd?'item2':'item1']">
						{{item.text}}
					</view>
				</view>
			</view>
			<view style="display:flex;flex-direction: row;margin-left: 30rpx;margin-right: 30rpx;margin-top:20rpx">
				<view v-if="index>3&&index<=7" :key="index" v-for="(item,index) in cartype" @click="carty(index)" style="flex-basis: 25%;display: flex;flex-direction: column;align-items: center;height:70rpx;">
					<view  :class="[cartype[index].confirmd?'item2':'item1']">
						{{item.text}}
					</view>
				</view>
			</view>
			<view style="display:flex;flex-direction: row;margin-left: 30rpx;margin-right: 30rpx;margin-top:20rpx">
				<view v-if="index>7&&index<=11" v-for="(item,index) in cartype" @click="carty(index)" style="flex-basis: 25%;display: flex;flex-direction: column;align-items: center;height:70rpx;">
					<view :class="[cartype[index].confirmd?'item2':'item1']">
						{{item.text}}
					</view>
				</view>
			</view>
			<view style="display:flex;flex-direction: row;margin-left: 30rpx;margin-right: 30rpx;margin-top:20rpx">
				<view v-if="index>11&&index<=15" v-for="(item,index) in cartype" @click="carty(index)" style="flex-basis: 25%;display: flex;flex-direction: column;align-items: center;height:70rpx;">
					<view :class="[cartype[index].confirmd?'item2':'item1']">
						{{item.text}}
					</view>
				</view>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;margin-top:40rpx;margin-left: 40rpx;margin-right: 40rpx;">
				<button class="bu" @click="sure">确认</button>
			</view>
			<!-- <u-icon label="选择准驾车型(可多选)" style="text-align: center;margin-top: 30rpx;font-size: 25rpx;font-weight: bold;"></u-icon> -->
		</u-popup>
		<u-picker mode="time" v-model="show2" :params="params" @confirm="confirm2"></u-picker>
		<u-picker mode="time" v-model="show3" :params="params" @confirm="confirm3"></u-picker>
		<u-modal v-model="show4" content="请补全表单"></u-modal>
		<u-modal v-model="show5" content="最多可选择三项"></u-modal>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				src:'/static/driver.png',
				ben:'您可以添加他人作为常用驾驶人，并进行管理，以便用车时选择',
				wheight:'',
				show:false,
				show1:false,
				show2:false,
				show3:false,
				show4:false,
				show5:false,
				have:false,
				// 记录选中的项数
				times:0,
				form:{
					name:'',
					tele:'',
					idcard:'',
					type:'',
					date1:'',
					date2:''
				},
				params:{
					year: true,
					month: true,
					day: true,
					hour: false,
					minute: false,
					second: false
				},
				usual:[],
				flag:-1,
				cartype:[
					{
						text:'A1',
						confirmd:false
					},
					{
						text:'A2',
						confirmd:false
					},
					{
						text:'A3',
						confirmd:false
					},
					{
						text:'B1',
						confirmd:false
					},
					{
						text:'B2',
						confirmd:false
					},
					{
						text:'C1',
						confirmd:false
					},
					{
						text:'C2',
						confirmd:false
					},
					{
						text:'C3',
						confirmd:false
					},
					{
						text:'C4',
						confirmd:false
					},
					{
						text:'C5',
						confirmd:false
					},
					{
						text:'D',
						confirmd:false
					},
					{
						text:'E',
						confirmd:false
					},
					{
						text:'F',
						confirmd:false
					},
					{
						text:'M',
						confirmd:false
					},
					{
						text:'N',
						confirmd:false
					},
					{
						text:'P',
						confirmd:false
					},
					
				]
			}
		},
		methods:{
			onShow(){
				this.wheight=(String)(uni.getSystemInfoSync().windowHeight*750/uni.getSystemInfoSync().windowWidth-40);
				console.log(this.wheight)
				this.usual=getApp().globalData.usual
				if(this.usual.length!=0)
				{
					this.have=false;
				}
				else{
					this.have=true;
				}
			},
			adduser(){
				for(var i=0;i<this.cartype.length;i++)
				{
					this.cartype[i].confirmd=false;
				}
				this.times=0;
				this.show=true;
				this.form.name='';
				this.form.tele='';
				this.form.type='';
				this.form.idcard='';
				this.form.date1='';
				this.form.date2='';
				
			},
			confirm2(res){
				var key1="year";
				// this.year=res[key];
				var key2="month";
				// this.month=res[key];
				var key3="day";
				// this.day=res[key];
				this.form.date1=res[key1]+'-'+res[key2]+'-'+res[key3]
			},
			confirm3(res){
				var key1="year";
				// this.year=res[key];
				var key2="month";
				// this.month=res[key];
				var key3="day";
				// this.day=res[key];
				// this.k=this.year+'-'+this.month+'-'+this.day;
				this.form.date2=res[key1]+'-'+res[key2]+'-'+res[key3]
			},
			car(){
				this.show1=true;
			},
			begin(){
				this.show2=true;
			},
			end(){
				this.show3=true;
			},
			complete(){
				if(this.form.name==''||this.form.name == null || this.form.name== undefined)
				{
					this.show4=true;
				}
				else if(this.form.tele==''||this.form.tele == null || this.form.tele== undefined)
				{
					this.show4=true;
				}
				else if(this.form.type==''||this.form.type == null || this.form.type== undefined)
				{
					this.show4=true;
				}
				else if(this.form.idcard==''||this.form.idcard == null || this.form.idcard== undefined)
				{
					this.show4=true;
				}
				else if(this.form.date1==''||this.form.date1 == null || this.form.date1== undefined)
				{
					this.show4=true;
				}
				else if(this.form.date2==''||this.form.date2 == null || this.form.date2== undefined)
				{
					this.show4=true;
				}
				else{
					var k;
						k=this.form;
						var d={
							name:'',
							tele:'',
							type:'',
							idcard:'',
							date1:'',
							date2:''
						};
						d.name=k.name;
						d.tele=k.tele;
						d.idcard=k.idcard;
						d.date1=k.date1;
						d.date2=k.date2;
						d.type=k.type;
						if(this.flag!=-1)
						{
							
							this.usual[this.flag]=d;
							this.flag=-1;
						}
						else{
							this.usual.push(d);
						}
						if(this.have==true)
						this.have=false
					this.show=false;
				}
					
			},
			people(index){
				var k=this.usual[index].type.split(",");
				for(var p=0;p<this.cartype.length;p++){
						this.cartype[p].confirmd=false;
						for(var i=0;i<k.length;i++){
							if(k[i]==this.cartype[p].text)
							{
								this.cartype[p].confirmd=true;
								break;
							}
						}
						
					}
			var d={
					name:'',
					tele:'',
					idcard:'',
					type:'',
					date1:'',
					date2:''
				};
				d.name=this.usual[index].name;
				d.tele=this.usual[index].tele;
				d.type=this.usual[index].type;
				d.idcard=this.usual[index].idcard;
				d.date1=this.usual[index].date1;
				d.date2=this.usual[index].date2;
				this.flag=index;
				this.form=d;
				this.show=true;
			},
			carty(index){
				
				if(this.cartype[index].confirmd==false){
					if(this.times<3){
					this.cartype[index].confirmd=true;
					this.times++
					}
					else{
						this.show5=true
					}
				}
				else{
				this.cartype[index].confirmd=false;
				this.times--;
				}
			},
			sure(){
				this.form.type='';
				if(this.times==0){
					
				}
				else{
					for(var i=0;i<this.cartype.length;i++)
					{
						if(this.cartype[i].confirmd==true)
						{
							this.form.type+=this.cartype[i].text;
							this.form.type+=',';
						}
					}
					this.form.type=this.form.type.substring(0,this.form.type.length-1)
					
				}
				this.show1=false;
			}
			
			
		}
		
	}
</script>

<style>
	page{
		background-color: #ebebeb;
	}
	.mid{
		/* margin-left:65rpx; */
		font-size:28rpx;
		margin-top:30rpx;
		font-weight: bold;
	}
	.tip{
		margin-top:40rpx;
		font-size:22rpx;
		text-align: center;
		color:#848484
	}
	.main{
		margin-left:180rpx;
		margin-top: 250rpx;
		margin-right:180rpx;
		display: flex;
		flex-direction:column;
		align-items: center;
	}
	.bottom{
	display:flex;
	height:140rpx;
	width:100%;
	bottom:0rpx;
	position:fixed;
	background-color:white;
	font-size:18rpx;
	}
	.ur{
		color:#FFFFFF;
		background-color: #18B566;
		line-height:90rpx;
		margin-top: 20rpx;
		height:90rpx;
		width:90%;
		font-size:30rpx;
		border-radius: 10;
	}
	.bu{
		/* display: flex; */
		background-color: #ff5500;
		color:white;
		height:80rpx;
		width:100%;
		font-size:28rpx;
		border-radius: 0rpx;
		line-height:80rpx;
		/* margin-left:12%;
		margin-top:15rpx;
		margin-bottom:15rpx; */
		/* margin-right:0rpx; */	
	}
	.item1{
		background-color: #efefef;width:90%;height:100%;text-align: center;line-height: 70rpx;font-size: 30rpx;
	}
	.item2{
		background-color: #ff5500;width:90%;height:100%;text-align: center;line-height: 70rpx;color:white;font-size: 30rpx;
	}
</style>
