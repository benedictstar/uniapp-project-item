<template>
	<view>
		<u-gap height="10" bg-color="#ebebeb" margin-bottom=""></u-gap>
		<u-cell-group>
			<u-cell-item title="开启地理位置定位" :value="loc" @click="locate"></u-cell-item>
			<u-gap height="15" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<view style="background-color:#ebebeb;font-size:23rpx;color:#848484;">
				<view style="margin-left: 30rpx;">
					<text>根据您的位置推荐您周围的车辆。关于</text>
					<text style="color:#ff5500;">《位置信息》</text>
				</view>
			</view>
			<u-gap height="50" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<u-cell-item title="允许来往租车访问相机" :value="cam" @click="camera"></u-cell-item>
			<u-gap height="15" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<view style="background-color:#ebebeb;font-size:23rpx;color:#848484;">
				<view style="margin-left: 30rpx;">
					<text>实现扫码、拍摄照片与上传。关于</text>
					<text style="color:#ff5500;">《访问相机》</text>
				</view>
			</view>
			<u-gap height="50" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<u-cell-item title="允许来往租车访问通讯录" :value="tel" @click="tele"></u-cell-item>
			<u-gap height="15" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<view style="background-color:#ebebeb;font-size:23rpx;color:#848484;">
				<view style="margin-left: 30rpx;">
					<text>方便您租车时取用您的联系人信息。关于</text>
					<text style="color:#ff5500;">《通讯录信息》</text>
				</view>
			</view>
			<u-gap height="50" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<u-cell-item title="允许来往租车访问相册" :value="pho" @click="album"></u-cell-item>
			<u-gap height="15" bg-color="#ebebeb" margin-bottom=""></u-gap>
			<view style="background-color:#ebebeb;font-size:23rpx;color:#848484;">
				<view style="margin-left: 30rpx;">
					<text>实现您图片的取用与上传。关于</text>
					<text style="color:#ff5500;">《访问相册》</text>
				</view>
			</view>
		</u-cell-group>
	</view>
</template>

<script>
	import permision from "@/js_sdk/wa-permission/permission.js"
	export default{
		data(){
			return{
				loc:'',
				tel:'',
				cam:'',
				pho:''
				
			}
		},
		methods:{
			onLoad(){
				// #ifdef APP-PLUS
				var platform;
				var root1,root2,root3,root4;
				uni.getSystemInfo({
					success:function (res){
						platform=res.platform
					}
				});
				console.log(platform);
				// if(platform=='ios'){
				// 	root1=permision.judgeIosPermission("location") //判断iOS上是否给予位置权限，有权限返回true，否则返回false
				// 	root2=permision.judgeIosPermission("camera") //判断iOS上是否给予相机权限，有权限返回true，否则返回false
				// 	root3=permision.judgeIosPermission("contact") //判断iOS通讯录，有权限返回true，否则返回false
				// 	root4=permision.judgeIosPermission("photoLibrary") //判断iOS上是否给予相册权限，有权限返回true，否则返回false
				// 	if(root1){
				// 		this.loc='已开启'
				// 	}
				// 	else{
				// 		this.loc='未开启'
				// 	}
				// 	if(root2){
				// 		this.cma='已开启'
				// 	}
				// 	else{
				// 		this.cma='未开启'
				// 	if(root3){
				// 		this.tel='已开启'
				// 	}
				// 	else{
				// 		this.tel='未开启'
				// 	}
				// 	if(root4){
				// 		this.pho='已开启'
				// 	}
				// 	else{
				// 		this.pho='未开启'
				// 	}
					
				// }
				if(platform=="android"){
					// root1=permision.requestAndroidPermission("android.permission.ACCESS_FINE_LOCATION")
					// root2=permision.requestAndroidPermission("android.permission.CAMERA")
					// root3=permision.requestAndroidPermission("android.permission.READ_CONTACTS")
					// root4=permision.requestAndroidPermission("android.permission.READ_EXTERNAL_STORAGE")
					permision.requestAndroidPermission("android.permission.ACCESS_FINE_LOCATION").then((res)=>{
						if(res==1){
							this.loc='已开启'
						}
						else{
							this.loc='未开启'	
						}
					})
					permision.requestAndroidPermission("android.permission.CAMERA").then((res)=>{
						if(res==1){
							this.cam='已开启'
						}
						else{
							this.cam='未开启'	
						}
					})
					permision.requestAndroidPermission("android.permission.READ_CONTACTS").then((res)=>{
						if(res==1){
							this.tel='已开启'
						}
						else{
							this.tel='未开启'	
						}
					})
					// if(permision.requestAndroidPermission("android.permission.READ_CONTACTS")){
					// 	this.tel='已开启'
					// }
					// else{
					// 	this.tel='未开启'
					// }
					permision.requestAndroidPermission("android.permission.READ_EXTERNAL_STORAGE").then((res)=>{
						if(res==1){
							this.pho='已开启'
						}
						else{
							this.pho='未开启'	
						}
					})
					// if(permision.requestAndroidPermission("android.permission.READ_EXTERNAL_STORAGE")){
					// 	this.pho='已开启'
					// }
					// else{
					// 	this.pho='未开启'
					// }
				}
				// #endif
				
			},
			locate(){
				// #ifdef MP-WEIXIN
				
				uni.authorize({
				    scope: 'scope.userLocation',
				    success() {
				        uni.getLocation()
				    }
				})
				console.log(1)
				// #endif
				// #ifdef APP-PLUS
				permision.gotoAppPermissionSetting()
				// #endif
				
				
			},
			album(){
				// #ifdef MP-WEIXIN
				uni.authorize({
				    scope: 'scope.camera',
				    success() {
				       
				    }
				})
				// #endif
				// #ifdef APP-PLUS
				permision.gotoAppPermissionSetting()
				// #endif
			},
			camera(){
				// #ifdef MP-WEIXIN
				uni.authorize({
				    scope: 'scope.camera',
				    success() {
				    }
				})
				// #endif
				// #ifdef APP-PLUS
				permision.gotoAppPermissionSetting()
				// #endif
			},
			tele(){
				permision.gotoAppPermissionSetting()
			}
			
		}
	}
</script>

<style>
	page{
		background-color: #ebebeb;
	}
</style>
