<template>
	<view class="all-page">


		<view class="title-box">
			<text class="title-message">{{title}}</text>
		</view>
		<view class="mian-box">
			{{content}}
		</view>
		<view class="customer-box">
			<view class="message1">没有解决问题?</view>
			<view class="entercustomer" @click="go_to_customer">咨询人工客服</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				content: "",
				title: ""
			};
		},
		methods: {
			go_to_customer() {

			}
		},
		onLoad: function(option) {
			const that = this
			const eventChannel = this.getOpenerEventChannel()
			eventChannel.emit('acceptDataFromOpenedPage', {
				data: 'test'
			});
			eventChannel.emit('someEvent', {
				data: 'test'
			});
			// 监听acceptDataFromOpenerPage事件，获取上一页面通过eventChannel传送到当前页面的数据
			eventChannel.on('acceptDataFromOpenerPage', function(data) {
				console.log("data",data.title)
				that.title=data.title
				that.content = data.content
			})
			
		}
	}
</script>

<style>
	.title-box {
		margin-top: 15rpx;
	}

	.title-message {
		font-size: 40rpx;
		font-weight: 700;
	}

	.customer-box {
		margin-top: 1000rpx;
	}

	.message1 {
		width: 100%;
		text-align: center;

	}

	.entercustomer {
		width: 100%;
		text-align: center;
		color: blue
	}
</style>
