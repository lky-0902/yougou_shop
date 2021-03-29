<template>
	<view class="cart">
		<view class="address">
			<button @click="addAddress()">添加收货地址</button>
		</view>
		<view class="title">
			<text>购物车</text>
		</view>
		<view class="list">
			<view class="list_item">
				<label>
					<checkbox color="#d4237a"/>
				</label>
				<image src="../../static/icon/logo.png" mode="widthFix"></image>
				<view class="pro_info">
					<view class="pro_description">介绍触发不上班是不被收入提高</view>
					<view class="price">
						<text style="color:#d4237a;font-weight: bold;">￥179</text>
						<view class="num_box">
							<uni-number-box :min="1"></uni-number-box>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="pay">
			<label>
				<checkbox color="#d4237a"/>全选
			</label>
			<view class="price">
				<view style="color:#d4237a;font-weight: bold;">￥179</view>
				<view style="font-size: 12px;">包含运费</view>
			</view>
			<button size="mini">结算({{1}})</button>
		</view>
	</view>
</template>

<script>
	import UniNumberBox from "../../uni_modules/uni-number-box/components/uni-number-box/uni-number-box.vue"
	export default {
		data() {
			return {
				
			}
		},
		components:{
			UniNumberBox
		},
		methods: {
			addAddress(){
				uni.navigateTo({
				    url: '/pages/address/address'
				});
			}
		}
	}
</script>

<style lang="scss">
.cart{
	height: 100vh;
	position: relative;
	.address{
		width: 100%;
		height: 120rpx;
		border-bottom: solid 2px #e30081;
		display: flex;
		align-items: center;
		button{
			width: 60%;
			height: 80rpx;
			line-height: 80rpx;
			color: #46c85b;
			border: solid 1px #46c85b;
			background-color: #fff;
		}
	}
	.title{
		height: 80rpx;line-height: 80rpx;
		font-size: 20px;
		font-weight: 700;
		border-bottom: solid 1px #e30081;
		text{
			margin-left: 20rpx;
		}
	}
	.list{
		overflow: scroll;
		.list_item{
			width: 100%;
			height: 200rpx;
			display: flex;
			border-bottom: solid 1px #cbcbcb;
			checkbox{
				margin-left: 10rpx;
				margin-top: 80rpx;
			}
			image{
				width: 160rpx;
				margin-left: 30rpx;
				margin-top: 20rpx;
			}
			.pro_info{
				.pro_description{
					width: 420rpx;
					height: 80rpx;
					margin-top: 20rpx;
					margin-left: 50rpx;
					font-size: 14px;
				}
				.price{
					width: 420rpx;
					height: 52rpx;
					margin-top: 20rpx;
					margin-left: 50rpx;
					position: relative;
					.num_box{
						display: inline-block;
						position: absolute;
						right: 0;
						bottom: 0;
					}
				}
			}
		}
	}
	.pay{
		width: 100%;
		height: 100rpx;
		position: absolute;
		bottom:0;
		border-top: 1px solid #cbcbcb;
		checkbox{
			margin-left: 10rpx;
			margin-top: 25rpx;
		}
		.price{
			margin-top: 10rpx;
			display: inline-block;
			position: absolute;
			right: 250rpx;
		}
		button{
			width: 240rpx;
			height: 100rpx;
			line-height: 100rpx;
			position: absolute;
			right: 0;
			background-color: #d4237a;
			border: none;
			border-radius: 0;
			color: #fff;
		}
	}
}
</style>
