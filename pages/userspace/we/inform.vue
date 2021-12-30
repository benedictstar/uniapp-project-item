<template>
	<view>
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<u-cell-group>
			<u-cell-item title="广州市互联网举报中心" value="" @click=""></u-cell-item>
			<u-cell-item title="违法和不良信息举报电话" value="12345"  @click="tele"></u-cell-item>
			<u-cell-item title="举报邮箱" value="" @click="mail"></u-cell-item>
		</u-cell-group>
		<u-modal v-model="show1" :content="content1" :show-cancel-button="true"
		 confirm-text="呼叫" @cancel="ca" @confirm=""></u-modal>
		 <u-modal v-model="show2" :content="content2"
		  confirm-text="确认"></u-modal>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				show1:false,
				content1:'是否拨打：12345',
				show2:false,
				content2:'举报邮箱：333@qq'
				
			}
		},
		methods:{
			tele(){
				this.show1=true
			},
			ca(){
				this.show1=false
			},
			mail(){
				this.show2=true
			}
		}
	}
</script>

<style>
</style>
