<template>
	<view class="search">
		<view class="search_box">
			<input type="text" v-model="query" class="search uni-input" confirm-type="search" placeholder="请输入要搜索的商品" @input="searchGoods()" />
		</view>
		<view class="lists">
			<view class="list_item" v-for="(item,index) in goodsList" :key="index" @click="toDetail(item.goods_id)">
				<view class="pro_info">
					<view class="pro_description">{{item.goods_name}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				query: "",
				goodsList:[]
			}
		},
		methods: {
			searchGoods() {
				uni.request({
					url: "https://api-hmugo-web.itheima.net/api/public/v1/goods/qsearch",
					data: {
						query: this.query
					},
					success: (res) => {
						console.log(res.data.message)
						this.goodsList = res.data.message
					}
				})
			},
			toDetail(id) {
				uni.navigateTo({
					url: '/pages/detail/detail?goods_id=' + id
				});
			},
		}
	}
</script>

<style lang="scss">
	.search {
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

		.lists {
			overflow: scroll;
			.list_item {
				width: 100%;
				height: 100rpx;
				display: flex;
				border-bottom: solid 1px #cbcbcb;
				.pro_info {
					.pro_description {
						margin: 20rpx 20rpx;
						font-size: 14px;
					}
				}
			}
		}
	}
</style>
