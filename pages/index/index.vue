<template>
	<view>
		<u-popup v-model="show_toast" mode="center"  >
			<view class="" @click="delete_toast" style="position: absolute; right: 15rpx; z-index: 999;">
				X
			</view>
			<view style="width: 700rpx;height:700rpx; margin: 0 auto; ">
				
				<image src="../../static/lingquanzhongxin.png" mode="" style="width: 100%; height: 700rpx;" @click="not_show_toast"></image>
			
			</view>
		</u-popup>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				show_toast: false
			}
		},
		onLoad()
		{
			this.show_toast=true;
		},
		methods:{
			delete_toast()
			{
				this.show_toast=false;
			},
			not_show_toast()
			{
				uni.navigateTo({
					url:'../coupon/coupon'
				})
				this.show_toast=false;
			}
		}
	}
</script>