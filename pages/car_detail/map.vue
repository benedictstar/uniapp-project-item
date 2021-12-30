<template>
	<view>
		<view style="height:1020rpx;width:100%;margin-bottom: 200rpx;">
			<map style="height:1020rpx;width:100%;margin-bottom: 200rpx;" :latitude="latitude" :longitude="longitude" :markers="covers"></map>
		</view>
		<view class="bottom">
			<view style="flex-basis: 60%;">
				<view class="title">位置</view>
				<view class="box-content">{{place}}</view>
			</view>		
		<u-icon name="map-fill" size="30" label="到这去" label-size="30" label-pos="left"
		color="#4690d5" label-color="#4690d5" style="margin-left: 10%;" @click="ju"></u-icon>
		</view>
	</view>
</template>

<script>
	export default {
	    data() {
	        return {
				place:'',//根据车主选定的地点动态的改变该值
				id:0, // 使用 marker点击事件 需要填写id
				title: 'map',
	            latitude: 23.0540551376,
	            longitude: 113.4130708748,
	            // 里面是标记点的经纬度即车所在地坐标
				covers: [{
							    latitude: 23.0540551376,
							    longitude: 113.4130708748,
							    iconPath: '../../../static/logo.png'
							}]
	        }
	    },
	    methods: {
			onLoad(res){
				this.place=res.place.replace(/""/g,"");
				this.place=JSON.parse(this.place)
			},
			//跳转到其他地图app
			ju(){
				
			}
	    }
	}
</script>

<style>
	.bottom{
	/* display:flex; */
	height:180rpx;
	width:100%;
	bottom:0rpx;
	position:fixed;
	background-color:white;
	font-size:18rpx;
	margin-left:50rpx;
	display:flex;
	}
	.title{
			font-size: 30rpx;
			font-weight: bolder;
			margin-top: 13rpx;
			
		}
		.box-content{
			font-size:25rpx;
			margin-top:20rpx;
			color:#585858;
			word-break: break-all;
			word-wrap: break-word;
			white-space: pre-line;
			
		}
</style>
