<template>
	<view class="content">
		<view>
			<image :src="goodInfo.imageUrl" mode=""></image>
		</view>
		<view>
		<text style="font-weight: bold; font-size: 32upx;">{{goodInfo.name}}\n</text>
		<text style="color: #555555; font-size: 24upx;" >{{goodInfo.count}}</text>
		</view>
		<view>
			<text>预计购买价格：</text>
			<text style="font-weight: bold; font-size: 28upx;">￥{{goodInfo.price}}\n</text>
		</view>
	</view>
</template>

<script>
	export default {
		props: ["goodInfo"],
		data() {
			return {

			};
		}
	}
</script>

<style>
	.content {
		display: flex;
		margin: 10upx;
		justify-content: space-around;
	}
	text{
		margin-top: 30upx;
	}
	image {
		height: 11vh;
		width: 10vw;
	}
</style>
