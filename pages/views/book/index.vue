<template>
	<view class="book">
		<view class="book-top">
			<!-- 顶部背景图 为了留白兼容苹果的刘海屏灵动岛等 -->
			<image class="top-bg" mode="center" src="@/static/images/book/top-bg.png"></image>
			<view class="book-title">预定</view>
		</view>
		<view class="main-box">
			<uni-segmented-control :current="current" :values="['麻将', '桌球']" style-type="button" active-color="#35956a"
				in-active-color="#fff" @clickItem="onClickItem" />
			<view>
				<view v-for="(item, index) in getPlayList" :key="index" class="card-box">
					<uni-card padding="0" spacing="0">
						<template v-slot:cover>
							<view class="custom-cover">
								<image class="cover-image" mode="center" :src="item.url">
								</image>
								<view class="cover-content">
									<view class="float-name">
										<view>{{ current === 0 ? "房间" : "桌号" }}：{{
                        item.name
                      }}</view>
										<view>{{ current === 0 ? "预定房间" : "预定球桌"
                      }}<uni-icons type="right" color="#fff" size="18"></uni-icons></view>
									</view>
								</view>
							</view>
						</template>
						<uni-list>
							<uni-list-item showArrow>
								<template v-slot:body>
									<view>{{ current === 0 ? "房间状态" : "球桌状态" }}：
										<uni-tag v-if="item.status === 0" text="空闲中，可预定" type="success" />
										<uni-tag v-if="item.status === 1"
											:text="`使用中,结束时间：${item.endTime.substring(11)}`" type="warning" />
									</view>
								</template>
							</uni-list-item>
							<uni-list-item v-if="item.tips && item.tips.length > 0">
								<template v-slot:body>
									<view>
										<uni-tag v-for="(tip, index) in item.tips" :key="index"
											style="margin-right: 8rpx" inverted :text="tip" type="success" />
									</view>
								</template>
							</uni-list-item>
							<uni-list-item v-if="item.cards && item.cards.length > 0">
								<template v-slot:body>
									<view class="card-list">
										<uni-tag v-for="(card, index) in item.cards" :key="index"
											style="margin-right: 8rpx" inverted :text="`${card.name}：￥${card.price}`"
											type="primary" />
									</view>
								</template>
							</uni-list-item>
						</uni-list>
					</uni-card>
					<image v-if="current === 0" class="book-mj-bg" mode="aspectFill"
						src="@/static/images/book/mj-bg.png"></image>
					<image v-else class="book-tq-bg" mode="aspectFill" src="@/static/images/book/tq-bg.png"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "",
		data() {
			return {
				current: 0,
				mjList: [{
						name: "天胡1",
						url: "/static/images/book/mjf1.jpg",
						status: 0,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						tips: ["wifi", "空调", "饮料", "零食"],
						cards: [{
								cardId: 1,
								name: "3小时套餐",
								price: 30,
							},
							{
								cardId: 2,
								name: "5小时套餐",
								price: 40,
							},
						],
					},
					{
						name: "地胡2",
						url: "/static/images/book/mjf1.jpg",
						status: 1,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						tips: ["wifi", "空调", "饮料", "零食"],
						cards: [{
								cardId: 1,
								name: "3小时套餐",
								price: 30,
							},
							{
								cardId: 2,
								name: "5小时套餐",
								price: 40,
							},
						],
					},
					{
						name: "十三幺3",
						url: "/static/images/book/mjf1.jpg",
						status: 1,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						tips: ["wifi", "空调", "饮料", "零食"],
						cards: [{
								cardId: 1,
								name: "3小时套餐",
								price: 30,
							},
							{
								cardId: 2,
								name: "5小时套餐",
								price: 40,
							},
						],
					},
				],
				zqList: [{
						name: "桌球1",
						url: "/static/images/book/zqf1.png",
						status: 0,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						tips: ["wifi", "空调", "饮料", "零食"],
						cards: [{
								cardId: 1,
								name: "3小时套餐",
								price: 30,
							},
							{
								cardId: 2,
								name: "5小时套餐",
								price: 40,
							},
						],
					},
					{
						name: "桌球2",
						url: "/static/images/book/zqf1.png",
						status: 1,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						tips: ["wifi", "空调", "饮料", "零食"],
						cards: [{
								cardId: 1,
								name: "3小时套餐",
								price: 30,
							},
							{
								cardId: 2,
								name: "5小时套餐",
								price: 40,
							},
						],
					},
					{
						name: "桌球3",
						url: "/static/images/book/zqf1.png",
						status: 1,
						beginTime: "2021-08-17 10:00:00",
						endTime: "2021-08-17 10:00:00",
						tips: ["wifi", "空调", "饮料", "零食"],
						cards: [{
								cardId: 1,
								name: "3小时套餐",
								price: 30,
							},
							{
								cardId: 2,
								name: "5小时套餐",
								price: 40,
							},
						],
					},
				],
			};
		},
		computed: {
			getPlayList() {
				return this.current === 0 ? this.mjList : this.zqList;
			},
		},
		methods: {
			// 点击切换tab
			onClickItem(e) {
				if (this.current !== e.currentIndex) {
					this.current = e.currentIndex;
					console.log("current", this.current);
				}
			},
		},
	};
</script>
<style scoped>
	.book {
		overflow-y: auto;
		height: 100vh;
		background-color: #eef9f5;
	}
	
	.book-top {
		width: 100%;
		height: 170rpx;
		position: relative;
	}
	
	.book-title {
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
		/* top: -65rpx; */
	}

	.card-box {
		position: relative;
	}

	.custom-cover {
		flex: 1;
		flex-direction: row;
		position: relative;
	}

	.cover-content {
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		height: 80rpx;
		background-color: rgba(0, 0, 0, 0.4);
		display: flex;
		flex-direction: row;
		align-items: center;
		padding-left: 30rpx;
		font-size: 32rpx;
		font-weight: bold;
		color: #fff;
	}

	.cover-image {
		width: 100%;
		height: 300rpx;
	}

	.float-name {
		width: 100%;
		display: flex;
		justify-content: space-between;
		font-weight: 400;
	}

	.card-list {
		display: flex;
	}

	.card-item {
		padding: 0 15rpx;
		font-size: 24rpx;
		background-color: #8ff6ce;
	}

	.book-mj-bg {
		width: 150rpx;
		height: 150rpx;
		position: absolute;
		bottom: 0;
		right: 40rpx;
	}

	.book-tq-bg {
		width: 165rpx;
		height: 130rpx;
		position: absolute;
		bottom: 20rpx;
		right: 60rpx;
	}
</style>