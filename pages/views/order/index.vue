<template>
	<view class="order">
		<!-- 头部用户信息 -->
		<view class="user-info">
			<view class="user-card">
				<view class="avatar-box">
					<view class="avatar">
						<image class="avatar-bg" src="@/static/images/order/avator.png" />
					</view>
					<view class="avatar-name">{{ userInfo.name }}</view>
				</view>
				<view class="balance-box">
					<view class="box-item">
						<view class="balance-title">余额</view>
						<view class="balance-num">10000</view>
					</view>
					<view class="box-item">
						<view class="balance-title">充值</view>
						<view class="balance-num">充200送50</view>
					</view>
					<view class="box-item">
						<view class="balance-title">积分</view>
						<view class="balance-num">10000</view>
					</view>
				</view>
				<view class="vip-level">vip1</view>
			</view>
		</view>
		<!-- 订单列表 -->
		<view class="order-list">
			<uni-segmented-control :current="current" :values="['进行中', '历史订单']" style-type="button"
				active-color="#42b983" in-active-color="#fff" @clickItem="onClickItem" />
			<!-- 进行中 -->
			<uni-collapse v-if="current === 0" ref="nowCollapse" v-model="nowValue" accordion
				@change="changeNowCollapse">
				<uni-collapse-item v-for="(item, index) in usingList" :key="index"
					:title="item.type === 1 ? `房名：${item.name}` : `桌名：${item.name}`" :thumb="
            item.type === 1
              ? '@/static/images/order/order-icon-mj.png'
              : '@/static/images/order/order-icon-tq.png'
          ">
					<view class="content">
						<view style="letter-spacing: 1rpx">起止时间：{{ item.beginTime }} - {{ item.endTime }}</view>
						<view style="
                margin-top: 20rpx;
                display: flex;
                justify-content: space-between;
              ">
							<view>订单状态：
								<uni-tag v-if="item.status === 1" text="进行中" type="success" />
								<uni-tag v-else text="已完成" type="primary" />
							</view>
							<view>积分：<text style="color: #42b983; font-weight: bold">待结算</text></view>
						</view>
					</view>
				</uni-collapse-item>
			</uni-collapse>
			<!-- 历史订单 -->
			<uni-collapse v-else ref="historyCollapse" v-model="historyValue" accordion @change="changeHisCollapse">
				<uni-collapse-item v-for="(item, index) in historyList" :key="index"
					:title="item.type === 1 ? `房名：${item.name}` : `桌名：${item.name}`" :thumb="
            item.type === 1
              ? '/static/images/order/order-icon-mj.png'
              : '/static/images/order/order-icon-tq.png'
          ">
					<view class="content">
						<view style="letter-spacing: 1rpx">起止时间：{{ item.beginTime }} - {{ item.endTime }}</view>
						<view style="
                margin-top: 20rpx;
                display: flex;
                justify-content: space-between;
              ">
							<view>订单状态：
								<uni-tag v-if="item.status === 1" text="进行中" type="success" />
								<uni-tag v-else text="已完成" type="primary" />
							</view>
							<view>积分：<text style="color: #42b983; font-weight: bold">+{{ item.score }}</text></view>
						</view>
					</view>
				</uni-collapse-item>
			</uni-collapse>
		</view>
	</view>
</template>

<script>
	export default {
		name: "",
		data() {
			return {
				userInfo: {
					name: "马喽1",
					remark: "喜欢清一色炸胡",
				},
				current: 0,
				nowValue: "0",
				historyValue: "",
				usingList: [{
					name: "地胡2",
					beginTime: "2021-08-17 10:00:00",
					endTime: "2021-08-17 10:00:00",
					status: 1,
					score: 100,
					type: 1,
				}, ],
				historyList: [{
						name: "天胡1",
						status: 0,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						score: 100,
						type: 1,
					},
					{
						name: "地胡2",
						status: 0,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						score: 100,
						type: 1,
					},
					{
						name: "丁俊晖1",
						status: 0,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						score: 100,
						type: 2,
					},
					{
						name: "清一色3",
						status: 0,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						score: 100,
						type: 1,
					},
					{
						name: "奥沙利文2",
						status: 0,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						score: 100,
						type: 2,
					},
					{
						name: "特鲁姆普3",
						status: 0,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						score: 100,
						type: 2,
					},
				],
			};
		},
		methods: {
			// 点击切换tab
			onClickItem(e) {
				if (this.current !== e.currentIndex) {
					this.current = e.currentIndex;
					console.log("current", this.current);
				}
			},
			// 点击折叠面板
			changeNowCollapse(e) {
				this.nowValue = e.value;
			},
			// 点击折叠面板
			changeHisCollapse(e) {
				this.historyValue = e.value;
			},
		},
	};
</script>
<style scoped>
	.order {
		width: 100%;
		height: 100vh;
		overflow-y: auto;
		background-color: #f4f4f4;
	}

	.user-info {
		width: 100%;
		height: 300rpx;
		background-color: #42b983;
		padding-top: 150rpx;
	}

	.user-card {
		width: 100%;
		height: 300rpx;
		background-color: #fff;
		border-radius: 20rpx;
		position: relative;
		top: 20rpx;
		padding-top: 20rpx;
	}

	.avatar-box {
		display: flex;
		margin: 0 20rpx;
	}

	.avatar {
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
		border: 8rpx solid #42b983;
	}

	.avatar-bg {
		width: 100%;
		height: 100%;
	}

	.avatar-name {
		height: 100rpx;
		line-height: 100rpx;
		font-size: 36rpx;
		font-weight: bold;
		margin-left: 20rpx;
	}

	.vip-level {
		position: absolute;
		top: 70rpx;
		right: 40rpx;
		width: 100rpx;
		height: 40rpx;
		background-color: #42b983;
		color: #fff;
		font-size: 32rpx;
		text-align: center;
	}

	.balance-box {
		display: flex;
		justify-content: space-between;
		margin: 30rpx 30rpx 0 30rpx;
	}

	.box-item {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.balance-title {
		font-size: 32rpx;
		font-weight: bold;
	}

	.balance-num {
		font-size: 28rpx;
		color: #9b9b9b;
		margin-top: 10rpx;
	}

	.order-list {
		margin-top: 60rpx;
		padding: 20rpx;
		background-color: #fff;
	}

	.content {
		padding: 20rpx;
	}
</style>