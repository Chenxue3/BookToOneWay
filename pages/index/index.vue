<template>
	<view class="content">
		<view class="top">
		</view>
		<view class="searchPart">
			<input class="seachBar" placeholder="搜索" />
		</view>
		<view class="swiperBar">
			<swiper class="swiper" circular indicator-dots=true autoplay=ture interval="2000" duration="500">
				<swiper-item>
					<image class="swiper-item" src="../../static/swiper/swiper0.jpg" mode="widthFix"></image>
				</swiper-item>
				<swiper-item>
					<image class="swiper-item" src="../../static/swiper/swiper1.png" mode="widthFix"></image>
				</swiper-item>
				<swiper-item>
					<image class="swiper-item" src="../../static/swiper/swiper2.jpg" mode="widthFix"></image>
				</swiper-item>
			</swiper>
		</view>
		<view class="mainPart">
			<view class="booksSell">
				<view class="titleItem" style="background-color: rgb(184, 231, 187);">
					<text class="iconfont icon-ershouwupin" style="font-size: 40upx; box-sizing: border-box; margin: 10upx;"></text>
					书籍选择
				</view>
				<view class="options">
					<view class="optionPart">
						<view class="iconfont icon-jurassic_entry-basicdata" style="font-size: 120upx;"></view>
						<button type="default" class="option" @click="funcTbc()">
							书籍录入
						</button>
					</view>
					<view class="optionPart">
						<view class="iconfont icon-shuji" style="font-size: 120upx;"></view>

						<button type="default" class="option" @click="goCart">书籍选择</button>
					</view>
				</view>
			</view>
			<view class="booksSell">
				<view class="titleItem" style="background-color: rgb(153, 215, 174);">
					<text class="iconfont icon-liebiaodaohang_gongyi" style="font-size: 40upx; border-box; margin: 10upx;"></text>
					公益捐书
				</view>
				<view class="options">

					<view class="optionPart">
						<view class="iconfont icon-xuexiao" style="font-size: 120upx;"></view>

						<button type="default" class="option" @click="funcTbc()">小学选读</button>
					</view>
					<view class="optionPart">

						<view class="iconfont icon-xuexiao1" style="font-size: 120upx;"></view>
						<button type="default" class="option" @click="funcTbc()">初中选读</button>
					</view>
					<view class="optionPart">

						<view class="iconfont icon-xuexiao2" style="font-size: 120upx;"></view>
						<button type="default" class="option" @click="funcTbc()">高中选读</button>
					</view>
				</view>
			</view>
			<view class="booksSell">
				<view class="titleItem" style="background-color: rgb(117, 204, 151);">
					<text class="iconfont icon-gongyimujuanhuodong" style="font-size: 40upx; border-box; margin: 10upx;"></text>
					公益报名
				</view>
				<view class="options">

					<view class="optionPart">

						<view class="iconfont icon-xinjianshou" style="font-size: 120upx;"></view>
						<button type="default" class="option" @click="funcTbc()">一封信</button>
					</view>

					<view class="optionPart">
<uni-icons type="book"></uni-icons>
						<view class="iconfont icon-huodong" style="font-size: 120upx;"></view>
						<button type="default" class="option" @click="funcTbc()">下乡去</button>
					</view>
					<view class="optionPart">

						<view class="iconfont icon-a-shipinduanshipinmeiti" style="font-size: 120upx;"></view>
						<button type="default" class="option" @click="funcTbc()">视频宣传</button>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		components: {
			// uniSearchBar
		},
		data() {
			return {}
		},
		onLoad() {

		},
		methods: {
			goCart() {
				uni.switchTab({
					url: "../cart/cart"
				})
			},
			funcTbc() {
				uni.showModal({
					title: "提示！",
					content: "功能尚未开发，敬请期待",
					showCancel: false
				})
			}

		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		background-color: #F0F0F0;
	}

	.top {
		background-image: linear-gradient(#08b263, #a1e0b1,#F0F0F0);
		background-color: rgb(178, 239, 193);
		width: 100%;
		height: 25vh;
	}

	.topBar {
		height: 80px;
		text-align: center;
		line-height: 80px;
		width: 100%;
		font-family: 'Courier New', Courier, monospace;
		font-size: 20px;
	}

	.searchPart {
		width: 90%;
		height: 30px;
		width: 90%;
		position: relative;
		z-index: 100;
		top: -23vh;
		border-radius: 15px;
	}

	.seachBar {
		background-color: rgb(220, 220, 220);
		border-radius: 15px;
		text-align: center;
		line-height: 30px;
	}

	.swiperBar {
		width: 90%;
		position: relative;
		z-index: 100;
		top: -20vh;
		border-radius: 15px;
		margin-bottom: -20px;
	}

	.mainPart {
		position: relative;
		top: -10vh;
	}

	.swiper-item {
		height: 50vh;
		text-align: center;
		width: 100%;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.booksSell {
		width: 100vw;
		margin-bottom: 20px;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}

	.optionPart {
		display: flex;
		flex-direction: column;
		height: 200upx;
		justify-content: space-around;
		justify-items: center;
		align-items: center;
	}

	.titleItem {
		background-color: #F8F8F8;
		width: 100%;
		height: 40px;
		font-size: 20px;
		line-height: 40px;
	}

	.options {
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		margin-top: 20px;
	}

	.option {
		font-size: 12px;
		width: 100px;
		background-color: none;
		border: 0px;
		/* background-image: linear-gradient(#F2F2F2, #a0e7cf); */
	}

	.icons {
		width: 35upx;
		height: 35upx;
	}
</style>
