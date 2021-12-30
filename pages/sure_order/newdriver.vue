<template>
	<view>
		<view class="" style="border-bottom-left-radius:30rpx; border-bottom-right-radius:30rpx; width:100%; background-color: #E35C31; height: 200rpx;">
			
		</view>
		<view style="border-radius: 30rpx; position: relative; top:-180rpx; background-color: white;width: 80%; margin: 0 auto;">
			<view class="" style="border-top-left-radius: 30rpx; border-top-right-radius: 30rpx; background-color: rgb(241,201,151); width: 100%; ">
				<view class="" style="font-size: smaller; margin-left: 20rpx; padding-top: 10rpx; padding-bottom: 10rpx;">
					*请确保姓名与证件一致
				</view>				
			</view>
			<view style="margin-left: 30rpx;margin-bottom: 30rpx;">
				<u-form :model="form" ref="uform" label-position="top">
					<u-form-item>
						<view class=""style="width: 90%; margin: 0 auto;">
							姓名
							<view class="" style="border-radius: 30rpx; border: 5rpx solid #F2F2F2; width: 100%;">
								<u-input placeholder="" v-model="form.name"  />
							</view>						
						</view>						
					</u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
					<u-form-item  label="证件类型">
						<u-radio-group v-model="va">
							<u-radio v-for="(item,index) in type" :key="index" :name="item.name" :disabled="item.disabled" active-color="#ff5500">
								{{item.name}}
							</u-radio>
						</u-radio-group>
					</u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
					<u-form-item>
						<view class=""style="width: 90%; margin: 0 auto;">
							证件号码
							<view class="" style="border-radius: 30rpx; border: 5rpx solid #F2F2F2; width: 100%;">
								<u-input placeholder="" v-model="form.idcard"  />
							</view>						
						</view>
					</u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
					<u-form-item>
						<view class=""style="width: 90%; margin: 0 auto;">
							联系手机
							<view class="" style="border-radius: 30rpx; border: 5rpx solid #F2F2F2; width: 100%;">
								<u-input placeholder="" v-model="form.tele"  />
							</view>						
						</view>
					</u-form-item>
					<u-gap height="4" bg-color="#e5e5e5" margin-bottom=""></u-gap>
				</u-form>
			</view>
		</view>
			<view class="bottom">
				<button class="bu" @click="commit">提交</button>
			</view>
	</view>
</template>

<script>
	import bottom4 from '../../components/bottom4.vue'
	export default{
		data(){
			return{
				label_style:{
					border:'1rpx solid solid'
				},
				form:{
					name:'',
					idcard:'',
					tele:'',
					cardname:'',
					disabled:false
				},
				va:'身份证',
				type:[
					{name:'身份证',
					disabled:false
					},
					{name:'护照',
					disabled:false,
					},
					{name:'回乡证',
					disabled:false,
					},
					{name:'台胞证',
					disabled:false,
					},
				]
			}
		},
		components: {
			bottom4,
			},
		methods:{
			commit(){
				if(this.form.name==''||this.form.idcard==''||this.form.tele=='')
				{
					
				}
				else{
					this.form.cardname=this.va;
					getApp().globalData.driverinf.unshift(this.form)
					uni.navigateBack({
						url:'changedriver'
					})
				}
			}
		}
	}
</script>

<style>
	page{
		background-color: #ebebeb;
	}
	.bottom{
	/* display:flex; */
	height:90rpx;
	width:120%;
	bottom:0rpx;
	position:fixed;
	font-size:18rpx;
	}
	.bu{
		/* display: flex; */
		background-color: #ff5500;
		color:white;
		height:64rpx;
		width:60%;
		text-align: center;
		font-size:28rpx;
		border-radius: 80rpx;
		margin-left:12%;
		margin-top:15rpx;
		margin-bottom:15rpx;
		/* margin-right:0rpx; */
		
		
	}
</style>
