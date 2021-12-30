<template>
	<view>
		<view class="nav">
			<u-navbar height="85" back-text="返回" title="费用明细" title-color="#000" >
				<view class="u-flex u-row-right" style="width: 100%;"><u-icon class="u-m-r-30" name="kefu-ermai" color="#000" size="48"></u-icon></view>
			</u-navbar>
		</view>
		<view class="content">
			<u-cell-group>
				<view>
					<view class="u-flex u-row-between u-p-26">
						<view>
							<view class="u-flex u-font-40 u-p-t-20">
								<view style="font-weight:600">预计消费:</view>
								<view class="u-m-l-50" style="color:#b42e26">509元</view>
							</view>
							<view class="u-flex u-p-t-20">
								<view>实付:</view>
								<view>509元</view>
							</view>
							<view class="u-font-12 u-p-t-20">(预计费用仅供参考，请以订单结算后的实际费用为准)</view>
						</view>
						<view style="color:#3ab398" @click="toPaymentRecord">付费记录</view>
					</view>
					<view class="u-flex u-row-between u-p-26">
						<view>基础费用</view>
						<view>509元</view>
					</view>
					<view class="u-flex u-row-between u-p-26">
						<view>押金</view>
						<view>4000元</view>
					</view>
				</view>
			</u-cell-group>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {};
	},
	methods: {
		toPaymentRecord() {
			uni.navigateTo({
				url: '/pages/details/paymentRecord'
			});
		}
	}
};
</script>

<style lang="scss"></style>
