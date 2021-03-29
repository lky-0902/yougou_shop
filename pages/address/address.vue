<template>
	<view class="address">
		<view class="status_bar"><!-- 这里是状态栏 --></view>
		<view class="nav">
			<text class="cancel" @click="cancel()">取消</text>
			<text class="choose">选择地址</text>
			<text class="confirm" @click="confirm()">确定</text>
		</view>
		<view class="container">
			<view class="address_list">
				<view class="list_item" v-for="item in addressList">
					<label>
						<checkbox color="#d4237a"/>
					</label>
					<view class="msg">
						<text>{{item.name}}</text></br>
						<text>{{item.addr}}</text>
					</view>
					<view class="iconfont icon-tishi"></view>
				</view>
			</view>
			<view>
				<button type="default">+</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				addressList:[
					// {
					// 	name:"张三",
					// 	addr:"北京市北京市西城区……"
					// },{
					// 	name:"李四",
					// 	addr:"北京市北京市东城区……"
					// }
				]
			}
		},
		methods: {
			cancel(){
				uni.navigateBack({
					url: '/pages/cart/cart'
				});
			},
			confirm(){
				
			}
		}
	}
</script>

<style lang="scss">
@import '../../static/icon/iconfont.css';
.address{
	.status_bar {
		height: var(--status-bar-height);
		width: 100%;
		background-color: #000000;
	}
	.nav{
		width: 100%;
		height: 100rpx;
		background-color: #000000;
		color: #fff;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		text{
			display: inline-block;
			margin-top: 50rpx;
		}
	}
	.container{
		position: relative;
		background-color: #eee;
		.address_list{
			position: relative;
			box-sizing: content-box;
			padding: 30rpx 0;
			.list_item{
				position: relative;
				// width: 100%;
				height: 90rpx;
				display: flex;
				background-color: #fff;
				font-size: 14px;
				margin-bottom:20rpx;
				checkbox{
					margin-left: 30rpx;
					margin-top: 20rpx;
					margin-right: 30rpx;
				}
				.msg{
					display: inline-block;
					padding-top: 5rpx;
				}
				.iconfont{
					display: inline-block;
					width: 50rpx;
					height: 50rpx;
					font-size: 25px;
					color: #d4237a;
					position: absolute;
					top: 20rpx;
					right: 40rpx;
				}
			}
		}
	}
}
</style>
