<template>
    <view>
        
    </view>
</template>

<script>
    import oneInput from '@/components/myp-one/myp-one.vue'

    export default {
        components: {
            oneInput
        },
        data() {
            return {
                
            }
        },
		onLoad()
		{
			
		},
        methods: {       
			test()
			{
				console.log("success!!!!!!!!!!!!!!!");
			}
        },
		onReady() {
		   setInterval(function()
		   {
		   	let that = this;
			let qq = new Date().getSeconds();
		   	uni.showModal({
		   	  
		   	    content: '您的停留时间过长，车型报价可能发生了变化，请重新获取报价',
		   		confirmText	:'重新获取报价',
		   		confirmColor:'blue',
		   		showCancel:false,
		   	    success: function (res) {
		   			uni.redirectTo({
		   				url:"./index.vue"
		   			})
		   	        if (res.confirm) {
		   	            console.log(qq);
		   	        } 
		   	    }
		   	});
		   }
		   ,5000);
		}
    }
</script>

<style>
</style>