<template>
	<view class="user">
		<view class="header">
			<view class="bg_img">
				<!-- 做模糊背景的图片 -->
				<image src="../../static/icon/logo.png" mode="aspectFill"></image>
			</view>
			<!-- 头像图片，应与上图保持一致 -->
			<image src="../../static/icon/logo.png" mode="widthFix"></image>
			<view class="name">追梦云彩</view>
		</view>
		<view class="collect">
			<view class="item">
				<text class="count">{{0}}</text>
				<text>收藏的店铺</text>
			</view>
			<view class="item">
				<text class="count">{{1}}</text>
				<text>收藏的商品</text>
			</view>
			<view class="item">
				<text class="count">{{0}}</text>
				<text>关注的商品</text>
			</view>
			<view class="item">
				<text class="count">{{0}}</text>
				<text>我的足迹</text>
			</view>
		</view>
		<view class="order">
			<view class="title">
				<text>我的订单</text>
			</view>
			<view class="detail">
				<view class="item">
					<view class="iconfont icon-wodedingdan"></view>
					<text>全部订单</text>
				</view>
				<view class="item">
					<view class="iconfont icon-daifukuan"></view>
					<text>待付款</text>
				</view>
				<view class="item">
					<view class="iconfont icon-daishouhuo"></view>
					<text>待收货</text>
				</view>
				<view class="item">
					<view class="iconfont icon-tuikuantuihuo"></view>
					<text>退款/退货</text>
				</view>
			</view>
		</view>
		<view class="address">
			<text @click="address()">收货地址管理</text>
		</view>
		<view class="other">
			<text>联系客服 <text id="phone">400-123-4567</text></text>
			<text>意见反馈</text>
			<text>关于我们</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		onLoad() {
			uni.getProvider({
				service: 'oauth',
				success: function(res) {
					console.log(res.provider)
					uni.login({
						provider: "weixin",
						success: function(loginRes) {
							console.log(loginRes.authResult)
							uni.getUserInfo({
								provider: 'weixin',
								success: function(infoRes) {
									console.log('用户昵称为：' + infoRes.userInfo.nickName);
								}
							});
						}
					})
				}
			});
		},
		methods: {
			address() {
				uni.navigateTo({
					url: '/pages/address/address'
				});
			}
		}
	}
</script>

<style lang="scss">
	@import '../../static/icon/iconfont.css';

	.user {
		height: 100vh;
		position: relative;
		background-color: #CCCCCC;

		.header {
			width: 100%;
			height: 40vh;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			position: relative;

			.bg_img {
				width: 100%;
				height: 100%;
				position: absolute;

				// z-index: -1;
				image {
					width: 100%;
					height: 100%;
					position: absolute;
					filter: blur(15px);
					// z-index: -1;
					border-radius: 0;
				}
			}

			image {
				width: 180rpx;
				border-radius: 90rpx;
				z-index: 999;
			}

			.name {
				margin-top: 50rpx;
				z-index: 999;
				color: #fff;
			}
		}

		.collect {
			width: 720rpx;
			height: 100rpx;
			margin: 0 15rpx;
			background-color: #fff;
			position: absolute;
			top: 400rpx;
			z-index: 999;
			display: flex;
			flex-direction: row;
			justify-content: space-around;

			.item {
				display: flex;
				flex-direction: column;
				align-items: center;
				font-size: 14px;
				margin-top: 10rpx;

				.count {
					color: #d4237a;
					font-weight: bold;
				}
			}
		}

		.order {
			width: 720rpx;
			height: 200rpx;
			margin: 0 15rpx;
			background-color: #CCCCCC;
			position: absolute;
			top: 515rpx;
			z-index: 999;

			.title {
				height: 75rpx;
				line-height: 75rpx;
				background-color: #fff;

				text {
					margin-left: 20rpx;
				}
			}

			.detail {
				height: 120rpx;
				margin-top: 5rpx;
				background-color: #fff;
				display: flex;
				flex: row;
				justify-content: space-around;

				.item {
					display: flex;
					flex-direction: column;
					justify-content: space-around;
					align-items: center;
					font-size: 14px;
					margin-top: 10rpx;

					.iconfont {
						font-size: 20px;
						color: #d4237a;
					}
				}
			}
		}

		.address {
			width: 720rpx;
			height: 80rpx;
			line-height: 80rpx;
			margin: 0 15rpx;
			background-color: #fff;
			position: absolute;
			top: 730rpx;
			z-index: 999;

			text {
				margin-left: 20rpx;
			}
		}

		.other {
			width: 720rpx;
			height: 250rpx;
			margin: 0 15rpx;
			background-color: #ccc;
			position: absolute;
			top: 825rpx;
			z-index: 999;

			text {
				display: block;
				height: 80rpx;
				line-height: 80rpx;
				background-color: #fff;
				padding-left: 20rpx;
				margin-top: 10rpx;

				#phone {
					position: absolute;
					right: 20rpx;
					top: 0;
				}
			}

		}
	}
</style>
