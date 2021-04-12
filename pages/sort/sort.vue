<template>
	<view class="sort">
		<view class="search_box">
			<input type="text" class="search" placeholder="搜索" @focus="toSearch()"/>
		</view>
		<view class="category">
			<scroll-view class="category_list" :scroll-top="scrollTop" scroll-y="true">
				<view class="list_item" v-for="item in categoryData">{{item.cat_name}}</view>
			</scroll-view>
			<scroll-view class="detail_category_list" :scroll-top="scrollTop" scroll-y="true">
				<view class="detail_list_item" v-for="(item,index) in categoryData" :key="index">
					<view class="title" v-for="data in item.children">
						<view>/ {{data.cat_name}} /</view>
						<view class="item_box">
							<view class="item" v-for="i in data.children" @click="toList(i.cat_id)">
								<image :src="i.cat_icon"></image>
								<view>{{i.cat_name}}</view>
							</view>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				categoryData: [],
				scrollTop: 0,
			}
		},
		onLoad() {
			this.getCategory()
		},
		methods: {
			toSearch(){
				uni.navigateTo({
				    url: '/pages/search/search'
				});
			},
			toList(cid){
				uni.navigateTo({
					url: '/pages/list/list?cid='+cid
				})
			},
			getCategory() {
				uni.request({
					// #ifdef MP-WEIXIN
					url: "https://api-hmugo-web.itheima.net/api/public/v1/categories",
					// #endif
					// #ifdef H5
					url: "/api/public/v1/categories",
					// #endif
					success: (res) => {
						console.log(res)
						this.categoryData = res.data.message
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.sort {
		height: 100vh;

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

		.category {
			display: flex;
			overflow: hidden;
			height: 90vh;

			.category_list {
				width: 22%;
				overflow: hidden;

				.list_item {
					height: 80rpx;
					text-align: center;
					line-height: 80rpx;
				}
			}

			.detail_category_list {
				width: 78%;
				overflow: hidden;

				.detail_list_item {
					.title {
						margin-top: 20rpx;
						text-align: center;

						.item_box {
							margin-left: 20rpx;
							display: flex;
							flex-direction: row;
							flex-wrap: wrap;

							// justify-content: space-around;
							.item {
								width: 100rpx;
								margin: 30rpx 40rpx;
								font-size: 12px;
								color: #3a3a3a;

								image {
									width: 100rpx;
									height: 100rpx;
								}
							}
						}
					}
				}
			}
		}
	}
</style>
