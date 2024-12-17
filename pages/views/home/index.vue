<template>
	<view class="home-box">
		<view class="home-top">
			<!-- 顶部背景图 为了留白兼容苹果的刘海屏灵动岛等 -->
			<image class="top-bg" mode="center" src="@/static/images/home/top-bg.png"></image>
			<view class="home-title">门店详情</view>
		</view>

		<view class="main-box">
			<!-- 顶部滚动通知 -->
			<uni-notice-bar class="notice-bar" show-icon scrollable text="自助桌球棋牌24小时营业，请提前预约，合理规划出行，遵纪守法，禁止赌博。" />
			<!-- 轮播简介图 -->
			<swiper class="swiper-box" autoplay :interval="interval" @change="change" :current="swiperDotIndex">
				<swiper-item v-for="(item, index) in bannerInfo" :key="index">
					<view class="swiper-item" :class="'swiper-item' + index">
						<image class="pic" mode="aspectFill" :src="item.url"></image>
					</view>
				</swiper-item>
			</swiper>

			<!-- 店铺基本信息 -->
			<view class="base-info">
				<view class="info-title">
					<view class="info-name">
						{{ baseInfo.name }}
						<uni-tag style="margin-left: 12rpx; font-size: 20rpx" inverted text="5星店铺" type="success" />
						<uni-tag style="margin-left: 12rpx; font-size: 20rpx" inverted text="24小时营业" type="success" />
					</view>
				</view>
				<view class="info-address" @click="copyAddress">
					<uni-icons type="location" size="20"></uni-icons>
					{{ baseInfo.address }}（点击地址可一键复制）
				</view>
			</view>

			<view class="common-funciton">
				<view class="func-item">
					<image class="fun-item-bg" mode="aspectFill" src="@/static/images/home/book.png"></image>
					<view class="func-item-title">预定棋牌</view>
				</view>
				<view class="func-item">
					<image class="fun-item-bg" mode="aspectFill" src="@/static/images/home/door.png"></image>
					<view class="func-item-title">开门进店</view>
				</view>
				<view class="func-item">
					<image class="fun-item-bg" mode="aspectFill" src="@/static/images/home/card.png"></image>
					<view class="func-item-title">美团验券</view>
				</view>
				<view class="func-item">
					<image class="fun-item-bg" mode="aspectFill" src="@/static/images/home/contact.png"></image>
					<view class="func-item-title">联系客服</view>
				</view>
			</view>

			<view class="btn-box">
				<button type="default" style="
            background-color: #42b983;
            color: #fff;
            font-weight: bold;
            font-size: 36rpx;
          ">
					您已预定，点此进入房间/球台 >>
				</button>
			</view>
		</view>

		<view class="enter-room">
			<view class="jm-box">
				<image class="jm-bg" mode="widthFix" src="@/static/images/home/jm.png"></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "",
		data() {
			return {
				swiperDotIndex: 0,
				interval: 3000,
				//店铺基础信息
				baseInfo: {
					name: "猴哥棋牌",
					address: "广东省中山市xxxxxxxxxxxxx楼C栋二楼212室",
					dealTime: "24小时",
					restSeat: 10,
					totalSeat: 25,
				},
				bannerInfo: [{
						colorClass: "uni-bg-red",
						url: "/static/images/home/mj1.png",
						content: "内容 A",
					},
					{
						colorClass: "uni-bg-green",
						url: "/static/images/home/mj2.png",
						content: "内容 B",
					},
					{
						colorClass: "uni-bg-blue",
						url: "/static/images/home/mj3.png",
						content: "内容 C",
					},
				],
			};
		},
		methods: {
			change(e) {
				this.swiperDotIndex = e.detail.current;
			},
			// 联系商家
			callManager() {
				const phoneNumber = "15622714165";
				uni.makePhoneCall({
					phoneNumber: phoneNumber, // 电话号码
					success: function() {
						uni.showToast({
							title: "拨打电话成功",
							duration: 2000,
						});
					},
					fail: function() {
						uni.showToast({
							title: "操作失败，请稍后重试",
							duration: 2000,
						});
					},
				});
			},
			// 开门进店
			openDoor() {},
			// 预定麻将/桌球
			book() {
				uni.switchTab({
					url: "/pages/views/book/index",
				});
			},
			// 一键复制地址
			copyAddress() {
				uni.setClipboardData({
					data: this.baseInfo.address,
					success: () => {
						uni.showToast({
							title: "复制成功",
							duration: 2000
						});
					},
					fail: () => {
						uni.showToast({
							title: "复制失败",
							icon: "none",
							duration: 2000
						});
					},
				});
			},
		},
	};
</script>
<style scoped>
	.home-box {
		background-color: #eef9f5;
		height: 100vh;
		overflow-y: auto;
	}
	
	.home-top {
		width: 100%;
		height: 170rpx;
		position: relative;
	}
	
	.home-title {
		width: 100%;
		text-align: center;
		color: #fff;
		font-weight: bolder;
		font-size: 40rpx;
		position: absolute;
		bottom: 30rpx;
	}

	.top-bg {
		width: 100%;
		height: 100%;
	}

	.main-box {
		position: relative;
		/* top: -90rpx; */
	}

	.notice-bar {
		margin-bottom: 0rpx !important;
	}

	.swiper-box {
		height: 350rpx;
	}

	.swiper-item {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 350rpx;
		color: #fff;
	}

	.pic {
		height: 100%;
		width: 100%;
	}

	.base-info {
		margin: 20rpx 24rpx;
		position: relative;
	}

	.info-title {
		display: flex;
		justify-content: space-between;
		height: 60rpx;
	}

	.info-name {
		font-size: 40rpx;
		line-height: 60rpx;
		font-weight: bold;
		color: #35956a;
	}

	.info-address {
		margin-top: 10rpx;
		font-size: 32rpx;
		color: #636363;
	}

	.info-time {
		margin-top: 24rpx;
		color: #42b983;
		font-size: 32rpx;
	}

	.common-funciton {
		padding: 0 40rpx;
		margin-top: 40rpx;
		display: flex;
		justify-content: space-between;
	}

	.func-item {
		width: 120rpx;
		height: 140rpx;
		border-radius: 20rpx;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.fun-item-bg {
		width: 100rpx;
		height: 100rpx;
		border-radius: 15rpx;
	}

	.func-item-title {
		width: 120rpx;
		font-size: 26rpx;
		height: 30rpx;
		line-height: 30rpx;
		margin-top: 10rpx;
		text-align: center;
	}

	.enter-room {
		width: 100%;
		position: fixed;
		bottom: 0;
	}

	.jm-box {
		width: 100%;
		height: 100rpx;
		border-radius: 20rpx;
		box-shadow: 0 0 10rpx rgba(0, 0, 0, 0.1);
	}

	.jm-bg {
		width: 100%;
		height: 200rpx;
		border-radius: 20rpx;
	}

	.btn-box {
		margin: 50rpx 30rpx 0 30rpx;
	}
</style>