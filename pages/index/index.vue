<template>
	<view class="index">
		<view class="search_box">
			<input type="text" class="search" placeholder="搜索" @focus="toSearch()" />
		</view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" class="swiper">
			<swiper-item v-for="(item,index) in swiperImage" :key="index">
				<image :src="item.image_src" @click="toDetail(item.goods_id)"></image>
			</swiper-item>
		</swiper>
		<view class="navbar">
			<image v-for="item in navImage" :src="item.image_src" mode="aspectFit" @click="toList(item.name)"></image>
		</view>
		<view class="floor">
			<view v-for="item in floorData">
				<image class="title" :src="item.floor_title.image_src" mode="aspectFit"></image>
				<view class="pro_item">
					<view class="big">
						<!-- 图片宽度不变，高度自动变化，保持宽高比 用widthFix-->
						<image :src="item.product_list[0].image_src" mode="widthFix" @click="toList(item.product_list[0].navigator_url)"></image>
					</view>
					<view class="small">
						<image :src="item.product_list[1].image_src" mode="scaleToFill" @click="toList(item.product_list[1].navigator_url)"></image>
						<image :src="item.product_list[2].image_src" mode="scaleToFill" @click="toList(item.product_list[2].navigator_url)"></image>
						<image :src="item.product_list[3].image_src" mode="scaleToFill" @click="toList(item.product_list[3].navigator_url)"></image>
						<image :src="item.product_list[4].image_src" mode="scaleToFill" @click="toList(item.product_list[4].navigator_url)"></image>
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
				swiperImage: [],
				navImage: [],
				floorData: {}
			}
		},
		onLoad() {
			this.getSwiper()
			this.getNavImage()
			this.getFloorData()
		},
		methods: {
			toDetail(id) {
				uni.navigateTo({
					url: '/pages/detail/detail?goods_id=' + id
				});
			},
			toList(name) {
				if (name == "分类") {
					console.log(name)
					uni.switchTab({
						url: '/pages/sort/sort'
					});
				} else if (name.length >= 23) {
					let params = name.slice(24)
					console.log(params)
					uni.navigateTo({
						url: '/pages/list/list?query=' + params
					});
				} else {
					let params = name.substr(0,name.length - 1)
					console.log(name)
					console.log(name.length)
					uni.navigateTo({
						url: '/pages/list/list?query=' + params
					});
				}
			},
			toSearch() {
				uni.navigateTo({
					url: '/pages/search/search'
				});
			},
			getSwiper() {
				uni.request({
					// #ifdef MP-WEIXIN
					url: "https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata",
					// #endif
					// #ifdef H5
					url: "/api/public/v1/home/swiperdata",
					// #endif
					success: (res) => {
						// console.log(res)
						this.swiperImage = res.data.message
					}
				})
			},
			getNavImage() {
				uni.request({
					// #ifdef MP-WEIXIN
					url: "https://api-hmugo-web.itheima.net/api/public/v1/home/catitems",
					// #endif
					// #ifdef H5
					url: "/api/public/v1/home/catitems",
					// #endif
					success: (res) => {
						// console.log(res)
						this.navImage = res.data.message
					}
				})
			},
			getFloorData() {
				uni.request({
					// #ifdef MP-WEIXIN
					url: "https://api-hmugo-web.itheima.net/api/public/v1/home/floordata",
					// #endif
					// #ifdef H5
					url: "/api/public/v1/home/floordata",
					// #endif
					success: (res) => {
						// console.log(res)
						this.floorData = res.data.message
					}
				})
			}

		}
	}
</script>

<style lang="scss">
	.index {
		width: 100%;
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

		.swiper {
			height: 400rpx;
			width: 100%;

			swiper-item image {
				width: 100%;
				height: 400rpx;
			}
		}

		.navbar {
			display: flex;
			justify-content: space-around;
			width: 100%;
			height: 200rpx;

			image {
				width: 150rpx;
				height: 190rpx;
			}
		}

		.floor {
			.title {
				width: 100%;
				height: 90rpx;
				margin: 0 20rpx;
			}

			.pro_item {
				display: flex;
				justify-content: center;

				.big {
					margin-right: 10rpx;
					width: 31%;

					image {
						width: 100%;
					}
				}

				.small {
					width: 62%;

					image {
						width: 48%;
						height: 190rpx;
						margin-right: 8rpx;
					}
				}
			}
		}
	}
</style>
