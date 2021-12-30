<template>
	<view>
		<view class="nav"><u-navbar height="85"  title="支付记录" title-color="#000" :title-bold="true"></u-navbar></view>
		<view class="content">
			<u-cell-group>
				<view class="u-p-26 u-border-bottom u-p-t-50">
					<view class="u-flex u-row-between u-font-32" style="font-weight:600;">
						<view>租车费用</view>
						<view>509元</view>
					</view>
					<view class="u-flex u-row-between" style="color:#a09ea1">
						<view>微信支付</view>
						<view>2021-07-02 13:48:17</view>
					</view>
				</view>
				<view class="u-flex u-row-between u-p-26 u-font-32" style="font-weight:600;">
					<view>押金</view>
					<view>4000元</view>
				</view>
<!-- 				<u-collapse 
				:head-style="headStyle">
				<u-collapse-item 
				title="押金 4000元"
				body="只要我们正确择取一个合适的参照物乃至稍降一格去看待他人，值得赏识的东西便会扑面而来"
				>				
				</u-collapse-item>
				</u-collapse> -->
			</u-cell-group>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
		};
	},
	methods: {}
};
</script>

<style></style>
