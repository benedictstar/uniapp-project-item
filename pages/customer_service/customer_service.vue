<template>
	<view>
		<view class="top">
		<!-- 	<view class="user-name-box">
				<view class="username">联系客服</view>
					<u-tag class="tag1" text="遇到问题请戳我" type="info" size="mini" shape="circle"></u-tag>
			</view> -->
			<view class="head-box">
				<view class="head"></view>
			</view>
			
			<view class="hello-box">
				<image class="hello" src="../../static/hello.png" mode="aspectFit"></image>
			</view>
			
			<view class="customer-box">
				<view class="customer-button"@click="go_to_talk_room">联系客服</view>
			</view>
		</view>
		
		<view class="mainner-box">
			
			<u-card class="tag-card" title="常见问题" title-color="#000000" title-size="35" padding="30" margin="15rpx" >
				<view class="item" slot = "body">
					<u-tag class="tag2" v-for="item in tagList" :key="item" :text="item" type="info" size="default" shape="circle" style="font-weight: normal;" @click="onClickTag(item)" />
				</view>

				<view class="item-detail" slot  = "foot">
					<view class="question-item"  v-for="(question, i) in question_id[selectTag]" :key="i" @click="go_to_question_detail(question.content,question.title)">
						<text>{{question.title}}</text>
					</view>	
				</view>
				
			</u-card>
			
		</view>

			
				
		</view>
	</view>
</template>
	
<script>
	export default{
		data(){
			return {
				request_id:'',
				selectTag: '',
				tagList: [
					'免押租车',
					'异地还车',
					'车辆出险',
					'车辆故障',
					'注册认证',
					'车辆网点',
					'支付订单',
					'取车环节',
					'还车环节',
					'发票获取',
					'违章处理',
					'修改订单',
				],
				question_id: uni.getStorageSync('question_id')
				// question_id:{
				// 	'免押租车':[
				// 		{
				// 			title:'123！'
				// 		},
				// 		{
				// 			title:'123124124124'	
				// 		}
				// 	]
				// }
			}
		},
		methods:{
			onClickTag (tag) {
				this.selectTag = tag;
				console.log(tag)
			},
			go_to_question_detail(content,title)
			{
				const that = this
				//调用云函数获取问题信息
				uni.navigateTo({
					url:'../question_detail/question_detail',
					events:{
						acceptDataFromOpenedPage:function(data){
							console.log(data)
						},
						someEvent: function(data) {
						      console.log(data)
						    }
					},
					//页面传参
					success:function(res) {
						res.eventChannel.emit('acceptDataFromOpenerPage',{content:content,title:title})
					}
				})
			},
			go_to_talk_room(){
				console.log("Gundan")
			}
		},
		onLoad() {
			//判断缓存中是否有question_id,没有则调用云函数并写入缓存
			if(this.question_id == ""){
				uniCloud.callFunction({
					name:"feedback",
					data:{
						"action":"search"
					}
				}).then(res=>{
					console.log("返回值",res.result.data[0].question_id)
					this.question_id = res.result.data[0].question_id
					console.log(JSON.parse(JSON.stringify(this.question_id)))
					uni.setStorageSync('question_id',this.question_id)
				})
			}
		}
	}
	
</script>

<style>
	
	.top{
		background-color: #ff5500;
		width: 100%;
		height: 500rpx;
		border-bottom-right-radius:60rpx;
		border-bottom-left-radius:60rpx;
		display: flex;
		justify-content: space-between;
	}
	
	.user-name-box{
		padding-top: 24px;
		padding-left: 55px;
	}
	.username{
		padding: 6px;
		color: #FFFFFF;
	}
	.item{
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
	}
	.tag1{
		margin-left: 10px;
		/* font-weight: bold; */
		
	}
	.tag2{
		font-weight: normal;
		margin-top: 2px;
		margin-bottom: 2px;
		color: #000000;
	}
	.tag2:hover{
		background-color: #E35c31;
		color: #FFFFFF;
		
	}
	
	.tag-card{
		font-weight: bold;
	}
	.mainner-box{
		/* min-height: 1200rpx; */
				/* background-color: #f8f8f8; */
				position: relative;
				top: -300rpx;
				border-radius: 60rpx;
				
				
	}
	.question-item{
		color: #696969;
		font-weight: normal;
		font-size: 12px;
		padding: 5px;
		
	}
	.question-item:not(:last-child){
		border-bottom: 1px solid #DCDCDC;
	}
	page{
		background-color:#F2F2F2;	
	}
	.head-box{
		width: 150rpx;
		height: 150rpx;
		background-color: #FFFFFF;
		margin-left: 20rpx;	
		margin-top: 30rpx;
		/* position: relative;
		top: 25rpx; */
		border-radius:50%;
	}
	.customer-box{
		width: 150rpx;
		height: 60rpx;
		background-color: #FFFFFF;
		border-radius: 30rpx;
		margin-top: 80rpx;
		margin-right: 25rpx;
	/* 	float: right;
		position: relative;
		top: -90rpx;
		right:20rpx; */
	}
	.customer-button{
		line-height: 60rpx;
		text-align: center;
		color: #E35C31;
		font-weight: bold;
	}
	.hello{
		width: 300rpx;
		height: 300rpx;
		
/* 		position: relative;
		top:-200rpx;
		left: 200rpx; */
	}
	.hello-box{
		margin-right: 110rpx;
		position: relative;
		top: -40rpx;
	}
	
</style>