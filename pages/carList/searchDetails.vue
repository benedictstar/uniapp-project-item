<template>
	<view class="u-p-26">
		<u-search placeholder="试试搜索品牌/车系" :focus="true" :show-action="false" height="100" shape="square" v-model="searchText" @search="searchStart"></u-search>
		<view v-if="searchText === ''">
			<!-- 搜索历史区域 -->
			<view v-if="historySearchList.length">
				<view class="u-flex u-p-t-46">
					<view class="title ">搜索历史</view>
					<u-icon name="trash-fill" size="38" class="u-m-l-26" @click="clearSearchCache"></u-icon>
				</view>
				<view class="u-flex u-flex-wrap">
					<u-tag v-for="item in historySearchList" @click="click_keyword(item)" :text="item" type="info"  shape="circle" color="#000" class="u-m-r-26 u-m-t-16" />
					</view>
			</view>
			<!-- 热门搜索区域 -->
			<view class="title u-p-t-46">热门搜索</view>
			<view class="u-flex u-flex-wrap ">
				<view v-for="(item, index) in hotSearchList"  class="u-flex u-p-t-40" style="width:50%;align-items:flex-start">
					<view style="width:15%;color:red" class="u-p-r-26 u-font-30">{{ index + 1 }}</view>
					<view @click="click_keyword(item.title)">
						<view style="font-weight:600">{{ item.title }}</view>
						<view style="color:gray">{{ item.description }}</view>
					</view>
				</view>
			</view>
		</view>
		<!-- 搜索推荐区域 -->
		<view v-else>
			<view v-for="item in recommendation" class="u-font-32 u-p-26 u-border-top">
				{{item}}
			</view>
		</view>
	</view>
</template>

<script>
export default {
	onShow() {
		try {
			const search_cache = uni.getStorageSync('search_cache');
			if (search_cache) {
				console.log(search_cache);
				this.historySearchList = search_cache;
				console.log('哈哈', this.historySearchList);
			}
		} catch (e) {
			// error
			console.log(e);
			console.log('获取缓存失败');
		}
	},
	data() {
		return {
			//搜索历史
			historySearchList: [],
			//搜索词
			searchText: '',
			//基于搜索词的搜索推荐
			recommendation:["基于搜索词的搜索推荐1","推荐2","推荐3","推荐4","推荐5","推荐6","推荐7"],
			//热门搜索，以index排序
			hotSearchList: [
				{
					title: '严选优车',
					description: '品质甄选,尊享18大特权'
				},
				{
					title: '严选优车2',
					description: '品质甄选,尊享18大特权'
				},
				{
					title: '严选优车3',
					description: '品质甄选,尊享18大特权'
				},
				{
					title: '严选优车4',
					description: '品质甄选,尊享18大特权'
				},
				{
					title: '严选优车5',
					description: '品质甄选,尊享18大特权'
				},
				{
					title: '严选优车6',
					description: '品质甄选,尊享18大特权'
				},
				{
					title: '严选优车7',
					description: '品质甄选,尊享18大特权'
				},
				{
					title: '严选优车8',
					description: '品质甄选,尊享18大特权'
				},
				{
					title: '严选优车9',
					description: '品质甄选,尊享18大特权'
				},
				{
					title: '严选优车10',
					description: '品质甄选,尊享18大特权'
				},
				{
					title: '严选优车11',
					description: '品质甄选,尊享18大特权'
				}
			]
		};
	},
	methods: {
		clearSearchCache() {
			this.historySearchList = [];
			uni.removeStorage({
				key: 'search_cache',
				success(res) {
					//sucess
				}
			});
		},
		clickTag(tagContent) {
			this.searchText = tagContent;
			try {
				uni.setStorageSync('storage_key', 'hello');
			} catch (e) {
				// error
			}
		},
		searchStart() {
			let _this = this;
			if (_this.searchText === '') {
				//搜索关键词为空
				uni.showToast({
					//提示信息
					title: '请输入关键字',
					icon: 'none',
					duration: 1000
				});
			} else {
				uni.getStorage({
					//从缓存中取搜索历史记录的数组
					key: 'search_cache',
					success(res) {
						//获取成功
						let list = res.data;
						for (let i in list) {
							//循环遍历
							if (list[i] == _this.searchText) {
								//如果缓存数组中有搜索关键词
								list.splice(i, 1); //删除数组中的该关键词
							}
						}
						list.unshift(_this.searchText); //将搜索关键词添加到数组开头
						list.splice(10); //只保留10个
						_this.historySearchList = list;
						uni.setStorage({
							//将新的数组存入缓存
							key: 'search_cache',
							data: _this.historySearchList
						});
						_this.search(_this.searchText); //搜索
					},
					fail() {
						//没有获取到缓存
						_this.historySearchList = [];
						_this.historySearchList.push(_this.searchText);
						uni.setStorage({
							key: 'search_cache',
							data: _this.historySearchList
						});
						_this.search(_this.searchText); //搜索
					}
				});
			}
		},
		search(value) {
			console.log('搜索内容:', value);
			console.log(this.historySearchList);
		},
		click_keyword(keyword)
		{
			getApp().globalData.search_keyword = keyword;
			uni.redirectTo({
				url:'/pages/carList/carList'
			})
		}
	}
};
</script>

<style></style>
