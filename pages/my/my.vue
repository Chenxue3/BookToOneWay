<!-- 
Description: “我的”页面
Author: XueshanChen
Date：2021/1/12
Version:1.0.0
Todo:！！注意处理了用户头像！之后要配置合法域名！
 -->
<template>
	<view style="width: 100vw;height: 100vh;">
		<view class="topBox">
			<view class="userImg">
				<image :src="userImageLocal" style="overflow: hidden"></image>
			</view>
			<view class="userInfo">
				<view class="nickName">
					测试用户
					<view class="vipTag" v-show="isVip">
						VIP
					</view>
					<view class="userInfoIcon" v-show="isLogin" @click="goUserInfoPage">
						>
					</view>
				</view>
				<!-- <view class="isLogin" v-show="!isLogin" @click="getUserInfo"> -->
				<!-- <login-btn @success="getUserInfo"></login-btn> -->
				<!-- </view> -->
			</view>
		</view>
		<view class="main">
			<view>
				<myPageitem content="积分商城" icon="iconfont icon-wodejifen"></myPageitem>
			</view>
			<view>
				<myPageitem content="会员中心" icon="iconfont icon-huiyuan"></myPageitem>
				<view>
					<myPageitem content="关于" icon="iconfont icon-guanyu"></myPageitem>
				</view>

			</view>
		</view>
	</view>
</template>
<script>
	// import loginBtn from "../../components/loginBtn.vue" //登录
	import myPageitem from "../../components/myPageItem.vue" //小条条
	export default {
		data() {
			return {
				userImageLocal:"../../static/tab-my.png"
			}
		},
		onShow() {},
		onLoad() {

		},
		components: {
			myPageitem
		},
		methods: {
			/**
			 * 生成微信临时图片(引用网络图片时需要将网络图片转换为微信临时本地地址)
			 * @param {String} 网络图片地址
			 */
			// handleNetImg(image) {
			// 	var that = this;
			// 	uni.getImageInfo({
			// 		src: image,
			// 		success: function(sres) {
			// 			that.userImageLocal = sres.path;
			// 			console.log(that.userImageLocal)
			// 		},
			// 		fail: () => {
			// 			console.log("处理头像失败！")
			// 		}
			// 	})
			// },
			
		}
	}
</script>

<style>
	page {
		background-color: rgb(238, 238, 238);
	}

	.topBox {
		background-color: #FFFFFF;
		height: 30%;
		margin-bottom: 10upx;
		padding-top: 40upx;
		position: relative;
		background-image: linear-gradient(#08b263, #a1e0b1,#F0F0F0);
	}

	.topBox>.userImg {
		width: 100%;
		height: 140upx;
		position: relative;
	}

	.topBox>.userImg>image {
		width: 140upx;
		height: 140upx;
		border-radius: 50%;
		position: absolute;
		left: 50%;
		transform: translateX(-50%);
		background-color: #808080;
	}

	.nickName {
		left: 50%;
		transform: translateX(-50%);
		height: 50upx;
		text-align: center;
		margin: 0upx;
		margin-top: 20upx;
		font-size: 30upx;
		position: absolute;
		display: flex;
		color: #FFFFFF;
	}

	.isLogin {
		margin-top: 20upx;
	}

	.vipTag {
		width: 40upx;
		height: 20upx;
		line-height: 20upx;
		border: RGBA(228, 156, 87, 1) 1upx solid;
		font-size: 19upx;
		margin: 0upx;
		margin-top: 10upx;
		background-color: RGBA(249, 210, 97, 1);
		color: RGBA(128, 62, 0, 1);
		border-radius: 15upx;
	}

	.userInfoIcon {
		width: 40upx;
		height: 20upx;
		font-size: 30upx;
		margin-left: 20upx;
	}

	.main {
		width: 90%;
		background-color: #fff;
		border-radius: 15upx;
		margin: 0 auto;
		padding: 20upx;
		position: fixed;
		left: 50%;
		transform: translateX(-50%);
		top: 320upx;

	}

	my-pageitems {
		width: 96%;
	}
</style>
