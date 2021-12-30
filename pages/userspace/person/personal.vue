<template>
	<view>
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<u-cell-group>
			<u-cell-item title="头像"  @click="header">
				<u-avatar :src="src" slot="right-icon" size="mini"></u-avatar>
			</u-cell-item>
			<u-cell-item title="昵称" :value="nickname" @click="nick"></u-cell-item>
			<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<u-cell-item title="性别" :value="sex" @click="show1=true"></u-cell-item>
			<u-cell-item title="生日" :value="k" @click="show2=true"></u-cell-item>
			<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<u-cell-item title="关于我" value="" @click="aboutme"></u-cell-item>
			<u-cell-item :title="introduce" value="" :arrow="false" @click="aboutme"></u-cell-item>
		</u-cell-group>
		<u-select v-model="show1" :list="list" @confirm="confirm1"></u-select>
		<u-picker mode="time" v-model="show2" :params="params" @confirm="confirm2"></u-picker>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				src:'',
				nickname:'',
				list: [{
						value: '1',
					label:'男',
					},
					{
						value: '2',
					label:'女',
					}
					
				],
				show1:false,
				show2:false,
				sex:'',
				params:{
					year: true,
					month: true,
					day: true,
					hour: false,
					minute: false,
					second: false
				},
				year:'',
				month:'',
				day:'',
				k:'',
				introduce:'',
				
			}
		},
		methods:{
			onShow(){
				this.introduce = uni.getStorageSync('introduce') || '';
				this.nickname = uni.getStorageSync('nickname') || '';
				this.avatar = uni.getStorageSync('avatar') || '';
				this.sex = uni.getStorageSync('sex') || '';
				this.k = uni.getStorageSync('birthday') || '';
			},
			nick(){
				uni.navigateTo({
					url:'./nickname'
				})
			},
			confirm1(res){
				this.sex=res[0].label;
				uni.setStorageSync('sex', this.sex);
				uniCloud.callFunction({
					name: "user-center",
					data: {
						action: "change",
						mobile: uni.getStorageSync('mobile'),
						sex: this.sex
					}
				})
			},
			confirm2(res){
				var key="year";
				this.year=res[key];
				key="month";
				this.month=res[key];
				key="day";
				this.day=res[key];
				this.k=this.year+'-'+this.month+'-'+this.day;
				uniCloud.callFunction({
					name: "user-center",
					data: {
						action: "change",
						birthday: this.k
					}
				})
			},
			aboutme(){
				uni.navigateTo({
					url:'./aboutme'
				})
			},
			header(){
				var that =this 
				uni.chooseImage({
					count: 1, //默认9
					sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album'], //从相册选择
				    success: function (res) {
				        console.log(JSON.stringify(res.tempFilePaths));
						this.src=res.tempFilePaths
						console.log(JSON.stringify(this.src));					
					}
			   })				
			}
			
			
		},
		onLoad() {

		}
	}
</script>

<style>
	page{
		background-color: #ebebeb;
	}
</style>
