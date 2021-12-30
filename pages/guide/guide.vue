<template>
	<view class="wrap">
			<swi :list="list" :title="true" :height="1000":effect3d="true" bg-color="#FF5500" mode="number" :autoplay="false" :current="0"></swi>
		</view>
</template>

<script>
	import swi from"../../components/u-swiper-new.vue"	
	export default{
		data(){	
			return{
				list: [{
							image: 'https://cdn.uviewui.com/uview/swiper/1.jpg',
							title: '昨夜星辰昨夜风，画楼西畔桂堂东',
							content:'12312123123123',
							bodycontent:'12312312321323'
						},
						{
							image: 'https://cdn.uviewui.com/uview/swiper/2.jpg',
							title: '身无彩凤双飞翼，心有灵犀一点通',
							content:'12312'
						},
						{
							image: 'https://cdn.uviewui.com/uview/swiper/3.jpg',
							title: '谁念西风独自凉，萧萧黄叶闭疏窗，沉思往事立残阳',
							content:'12312'
						}
						],
				}
				},
				
		components:{
			swi
		
			}
		}

	
</script>

<style>
	.wrap /deep/ .u-swiper-title{
		/* 总体文本框 */
		height: 300rpx;
		background-color: #FFFFFF;
		
	} 
	.wrap /deep/ .u-line-1{
		color: #F0AD4E;
	}
	
	.wrap{
		padding: 100rpx;
		margin-top: 100rpx;
		border-radius:20% ;
	}
	/* 修改content样式需要在u-swiper-new组件修改 */
</style>
x