<template>
	<view class="list">
		<view class="search_box">
			<input type="text" class="search" placeholder="搜索" @focus="toSearch()" />
		</view>
		<view class="order">
			<text>综合</text>
			<text>销量</text>
			<text>价格</text>
		</view>
		<view class="lists">
			<view class="list_item" v-for="(item,index) in goodsList" :key="index">
				<image :src="item.goods_big_logo" mode="widthFix"></image>
				<view class="pro_info">
					<view class="pro_description">{{item.goods_name}}</view>
					<view class="price">
						<text style="color:#d4237a;font-weight: bold;">￥{{item.goods_price}}</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				goodsList: [],
				cid:9
			}
		},
		onLoad() {
			this.getList()
		},
		methods: {
			toSearch() {
				uni.navigateTo({
					url: '/pages/search/search'
				});
			},
			getList() {
				uni.request({
					url: "https://api-hmugo-web.itheima.net/api/public/v1/goods/search",
					data: {
						cid: this.cid
					},
					success: (res) => {
						console.log(res.data.message.goods)
						this.goodsList = res.data.message.goods
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.list {
		.search_box {
			background-color: #d4237a;
			width: 100%;
			height: 100rpx;
			// text-align: center;
			box-sizing: border-box;
			padding-top: 20rpx;

			.search {
				background-color: #fff;
				width: 710rpx;
				height: 60rpx;
				border-radius: 10rpx;
				margin-left: 20rpx;
			}
		}

		.order {
			width: 100%;
			height: 80rpx;

			text {
				width: 33.3%;
				height: 80rpx;
				line-height: 80rpx;
				display: inline-block;
				text-align: center;
				border-bottom: 1px solid #CCCCCC;
			}
		}

		.lists {
			overflow: scroll;

			.list_item {
				width: 100%;
				height: 200rpx;
				display: flex;
				border-bottom: solid 1px #cbcbcb;

				image {
					width: 160rpx;
					margin-left: 30rpx;
					margin-top: 20rpx;
				}

				.pro_info {
					.pro_description {
						width: 420rpx;
						height: 80rpx;
						margin-top: 20rpx;
						margin-left: 50rpx;
						font-size: 14px;
					}

					.price {
						width: 420rpx;
						height: 52rpx;
						margin-top: 40rpx;
						margin-left: 50rpx;
						position: relative;
					}
				}
			}
		}
	}
</style>
