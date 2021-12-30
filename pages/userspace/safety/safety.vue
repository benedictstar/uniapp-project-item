<template>
	<view>
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<u-cell-group>
			<u-cell-item title="换绑手机号" :value="number" @click="change"></u-cell-item>
			<u-cell-item title="绑定微信" value="租金押金可减免20%"></u-cell-item>
			<u-cell-item title="更改手机密码" value="" @click="reset"></u-cell-item>
			<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<u-cell-item title="注销账号" value="注销后无法恢复,请谨慎操作" @click="cancel"></u-cell-item>
		</u-cell-group>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				number:'',
			}
		},
		methods:{
			onShow(){
				var k;
				k=getApp().globalData.numbers;
				for(var i=0;i<k.length;i++)
				{
					if(i<=2||i>=7)
					this.number+=k[i]
					else
					this.number+='*'
				}
			},
			change(){
				uni.navigateTo({
					url:'./changetele'
				})
			},
			reset(){
				uni.navigateTo({
					url:'./reset'
				})
			},
			cancel(){
				uni.navigateTo({
					url:'./cancel'
				})
			}
			
		}
		
	}
</script>

<style>
	page{
		background-color: #ebebeb;
	}
</style>
