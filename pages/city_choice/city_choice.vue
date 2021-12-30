<template>	
	<view>
		<t-city @from_son_to_father="back_to_main_page" />		
	</view>
</template>

<script>
	//引入组件
	 import TCity from '../../citySelect/components/t-city.vue';
	//注册组件
	export default {
		data:{
			return:{
				is_from_place:0,
				is_from_main:0
			}
		},
	    components:{
			't-city':TCity
	    },
		onLoad(e){
		},
	    methods:{
			back_to_main_page(e)
			{										
				if(getApp().globalData.is_from_main==1)
				{	
				getApp().globalData.city_choice = e.city_choice;
				getApp().globalData.is_from_main=0;
				uni.switchTab({
					url:"../mian_page/mian_page",					
				})		
				}
				else if(getApp().globalData.is_from_place==1)
				{
				getApp().globalData.is_from_place=0;
				uni.redirectTo({
						url:'../place_choice/place_choice'						
					})
				}
				else if(getApp().globalData.is_from_main_return==1)
				{
					getApp().globalData.city_choice_return = e.city_choice;
					getApp().globalData.is_from_main_return=0;
					uni.switchTab({
						url:"../mian_page/mian_page",					
					})
				}
				else if(getApp().globalData.is_from_coupon==1)
				{
					getApp().globalData.city_choice_coupon = e.city_choice;
					getApp().globalData.is_from_coupon=0;
					uni.redirectTo({
				       url:'../coupon/coupon'
				    })
				}
				else if(getApp().globalData.is_from_carList==1)
				{
					getApp().globalData.city_choice_carList = e.city_choice;
					getApp().globalData.is_from_carList=0;
					uni.redirectTo({
					   url:'../carList/carList'
					})
				}
			}
	    }
	}
</script>

<style>

</style>
