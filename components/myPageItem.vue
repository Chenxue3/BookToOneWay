<!-- 
Description: “我的”页面选项条组件
Author: XueshanChen
Date：2021/1/12
Version:1.0.0
Todo:传入“content”，对应在这个条条内显示对应的内容
传入“icon”，对应icon
 -->

<template>
	<view class="">
		<view class="container">
			<view class="greyRect">
				<image :src="icon" mode=""></image>
			</view>
			{{content}}
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		},
		props: ['content', "icon"],
	}
</script>

<style>
	.container {
		box-sizing: border-box;
		background-color: #fff;
		width: 100%;
		height: 85upx;
		padding-top: 24upx;
		display: flex;
		border-bottom: 1upx solid #999999;
	}

	.greyRect>image {
		width: 35upx;
		height: 35upx;
		background-color: rgb(232, 233, 232);
		border: #C0C0C0 solid 1upx;
		margin-left: 50upx;
		margin-right: 50upx;
	}
</style>
