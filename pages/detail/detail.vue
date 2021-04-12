<template>
	<view class="detail">
		<view class="img">
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" style="height: 250px;">
				<swiper-item v-for="(item,index) in goodsDetailList.pics" :key="index">
					<image :src="item.pics_mid" mode="aspectFit" style="margin-left: 28px;"></image>
				</swiper-item>
			</swiper>
		</view>
		<view class="info">
			<view class="price" style="color:#d4237a;font-weight: bold;">￥{{goodsDetailList.goods_price}}</view>
			<view class="desc">{{goodsDetailList.goods_name}}</view>
			<view class="collect"></view>
		</view>
		<view class="title">图文详情</view>
		<view class="introduce" v-html="introduce">
		</view>
		<view class="bottom">
			<view class="chat item">联系客服</view>
			<view class="share item">分享</view>
			<view class="cart item">购物车</view>
			<view class="addCart item" @click="addCart()">加入购物车</view>
			<view class="buy item">立即购买</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				goods_id: 57445,
				goodsDetailList: [],
				introduce: ""
			}
		},
		onLoad(data) {
			this.goods_id = data.goods_id
			this.showGoodDetail()
		},
		methods: {
			showGoodDetail() {
				uni.request({
					url: "https://api-hmugo-web.itheima.net/api/public/v1/goods/detail",
					data: {
						goods_id: this.goods_id
					},
					success: (res) => {
						console.log(res.data.message)
						this.goodsDetailList = res.data.message
						this.introduce = res.data.message.goods_introduce
					}
				})
			},
			addCart() {
				uni.$emit("add", {
					msg: this.goods_id
				})
				console.log("加入成功")
			}
		}
	}
</script>

<style lang="scss">
	.detail {
		background-color: #dfdfdf;

		.img {
			background-color: #fff;
		}

		.info {
			background-color: #fff;

			.price {
				color: #d4237a;
				font-weight: bold;
				margin: 0 20rpx;
				font-size: 20px;
			}

			.desc {
				margin: 0 20rpx;
			}
		}

		.title {
			height: 80rpx;
			line-height: 80rpx;
			margin: 15rpx 0;
			padding: 0 20rpx;
			background-color: #fff;
			z-index: 999;
			font-size: 18px;
			color: #d4237a;
			font-weight: bold;
		}

		.introduce {
			margin: 0 15rpx 100rpx;
		}

		.bottom {
			width: 100%;
			height: 100rpx;
			line-height: 100rpx;
			display: flex;
			justify-content: center;
			position: fixed;
			bottom: 0;
			background-color: #fff;
			font-size: 14px;

			.item {
				text-align: center;
			}

			.chat {
				width: 150rpx;
			}

			.share {
				width: 100rpx;
			}

			.cart {
				width: 150rpx;
			}

			.addCart {
				width: 175rpx;
				background-color: #EE9900;
				color: #fff;
				font-weight: bold;
			}

			.buy {
				width: 175rpx;
				background-color: #d4237a;
				color: #fff;
				font-weight: bold;
			}
		}
	}
</style>
