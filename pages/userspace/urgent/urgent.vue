<template>
	<view>
		<u-navbar title="紧急联系人"></u-navbar>
		<view v-if="have">
			<view class="main">
				<image :src="src" style="width:200rpx;height:200rpx;"></image>
				<view class="mid">请添加紧急联系人信息</view>
				<view class="tip">{{ben}}</view>
			</view>
		</view>
		<view v-else="have">
			<view style="margin-left: 30rpx;margin-right: 30rpx;margin-top: 10rpx;color:#909090;
			font-size:25rpx">{{ben}}</view>
			<u-cell-group>
				<u-cell-item v-for="(item,index) in urgent" :key="index" :title="item.name" :value="item.tele" :index="index" @click="people"></u-cell-item>
			</u-cell-group>
		</view>
		<view class="bottom">
			<button class="ur" @click="add">添加紧急联系人</button>
		</view>
		<u-popup mode="bottom" :height="wheight" :closeable="true" v-model="show" close-icon-pos="top-left" :mask="false">
			<view style="font-weight: bold;margin-top:100rpx;font-size:40rpx;margin-left:25rpx">请填写紧急联系人的信息</view>
			<view style="margin:40rpx">
				<u-form ref="uForm" :model="form">
					<u-form-item label="姓名"><u-input :clearable="false" placeholder="请输入姓名" v-model="form.name"></u-input></u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
					<u-form-item label="手机号">
						<u-input :clearable="false" placeholder="请输入手机号" v-model="form.tele" maxlength="11"/>
					</u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
				</u-form>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;margin-top:80rpx;margin-left: 40rpx;margin-right: 40rpx;">
				<button class="bu" @click="complete">完成</button>
			</view>
		</u-popup>
		<u-modal v-model="show1" :content="content1"></u-modal>
		<u-modal v-model="show2" :content="content2"></u-modal>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				src:'/static/addusergroup.png',
				ben:'为了保证您的行程安全，请至少添加1位紧急联系人，别让您最爱的人担心',
				show:false,
				wheight:'',
				//模态框的设置
				show1:false,
				content1:'请填写姓名',
				show2:false,
				content2:'请填写手机号',
				//用flag来判断是新增还是修改，0是新增，1是修改
				flag:-1,
				have:false,
				form:{
					name:'',
					tele:''
				},
				urgent:[
					// {
					// 	name:'h',
					// 	tele:'123',
					// },
					
				]
			}
		},
		methods:{
			onShow(){
				this.wheight=(String)(uni.getSystemInfoSync().windowHeight*750/uni.getSystemInfoSync().windowWidth-40);
				this.urgent=getApp().globalData.urgent
				if(this.urgent.length!=0)
				{
					this.have=false;
				}
				else{
					this.have=true;
				}
			},
			add(){
			this.form.name='';
			this.form.tele='';
			this.show=true;
			},
			complete(){
				if(this.form.name==''||this.form.name == null || this.form.name== undefined)
				{
					this.show1=true;
				}
				else if(this.form.tele==''||this.form.tele == null || this.form.tele== undefined)
				{
					this.show2=true;
				}
				else{
					if(this.flag!=-1)
					{
						var k;
						k=this.form;
						var d={
							name:'',
							tele:'',
						};
						d.name=k.name;
						d.tele=k.tele;
						this.urgent[this.flag]=d;
						this.flag=-1;
					}
					else{
						var k;
						k=this.form;
						var d={
							name:'',
							tele:'',
						};
						d.name=k.name;
						d.tele=k.tele;
						this.urgent.push(d);
					}
					if(this.have==true)
					this.have=false
					this.show=false;
				}
				
			},
			people(index){
				var d={
					name:'',
					tele:'',
				};
				d.name=this.urgent[index].name;
				d.tele=this.urgent[index].tele;
				this.flag=index;
				this.form=d;
				this.show=true;
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
</style>
