<template>
	<view class="content">
		<scroll-view class="menu-wrapper" scroll-y :scroll-top="left_scroll" scroll-with-animation="true">
			<view class="left-content">
				<view style="position: relative;" v-for="(item,index) in goods" :key="index" ref="menuList"
					@click="select(index)" :class="{'current': currentIndex == index}">
					<view class="menu-item">{{item.name}}</view>
					<text class="allcount" v-if="getAllCount>=item.count&&item.count>0">{{item.count}}</text>
				</view>
			</view>
		</scroll-view>
		<!-- 右侧滚动 -->
		<scroll-view class="foods-wrapper" scroll-y :style="'height:'+windows_height+'px'" :scroll-top="foodSTop"
			@scroll="myscroll" scroll-with-animation="true">
			<view ref="foodsWrapper">
				<view ref="foodList" class="foods" v-for="(item, i) in goods" :key="i">
					<view class="food-title" style="background: #f3f5f7">
						{{item.name}}
					</view>
					<view class="food" v-for="(food, index) in item.foods" :key="index">
						<image :src="food.imageUrl" mode="" style="width: 75px;height: 75px;margin-top: 6px;"></image>
						<view class="food-info">
							<text style="font-size: 15px;margin-top: 2px;">{{food.name}}</text>
							<text style="font-size: 13px;margin: 2px 0;">剩余：{{food.remark}}</text>
							<!-- <text style="font-size: 13px;margin: 2px 0 4px;">月售{{food.sellCount}}</text> -->
							<!-- 加减 -->
							<view class="food-btm">
								<text class="food-price">￥{{food.price}}</text>
								<cartcontrol :food="food" @add="addCart" @dec="decreaseCart"></cartcontrol>
							</view>
						</view>
					</view>
				</view>
			</view>
		</scroll-view>
		<shopcart :goods="goods" @add="addCart" @dec="decreaseCart" @delAll="delAll"></shopcart>
	</view>
</template>

<script>
	import shopcart from '@/components/shopcart.vue';
	import cartcontrol from '@/components/cartcontrol.vue'
	// import goods from "../../static/books/goods.js"
	import Vue from 'vue'

	export default {
		data() {
			return {
				mealType: "",
				mealTypeList: ["建工", "信自", "电力", "机电", "法学", "艺传统", "农工", "医学院"],

				windows_height: 0, //屏幕高度
				foodSTop: 0, //右侧的滑动值
				currentIndex: 0,
				goods: [],
				last: 0,
				right_height: [], //右侧每个内容的高度集合
				select_index: 0,
				left_height: 0, //左侧总高度
				left_scroll: 0, //左侧滑动值
				catrgoryList: [],
				timeout: null,
				goods: [{
						"id": 1,
						"name": "建工学院",
						"foods": [{
								"name": "毛泽东思想和中国特色社会主义理论体系概论（2021年版）",
								"remark": 20,
								"price": 25,
								"imageUrl": "https://img14.360buyimg.com/pop/jfs/t1/184033/39/21231/68054/612b1c6eE48d84278/3e0f3d30986b88ef.jpg"
							},
							{
								"name": "BIM技术原理及应用",
								"remark": 20,
								"price": 50,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jg_bim.jpg"
							},
							{
								"name": "多元统计分析及R语言建模（第五版）",
								"remark": 20,
								"price": 56,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jg_rjm.jpg"
							},
							{
								"name": "钢结构(第五版)",
								"remark": 20,
								"price": 39,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jg_gjg.jpg"
							},
							{
								"name": "结构设计原理(第4版)",
								"remark": 20,
								"price": 35,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jg_jgsjyl.jpg"
							},
							{
								"name": "工程经济学",
								"remark": 20,
								"price": 48,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jg_gcjjx.jpg"
							},
							{
								"name": "工程项目管理(第二版)",
								"remark": 20,
								"price": 49,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jg_gcxmgl.jpg"
							},
							{
								"name": "建筑结构设计软件PKPM2010应用与实例",
								"remark": 20,
								"price": 55,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jg_pkpm.jpg"
							},
							{
								"name": "建筑结构选型（第二版）（赠课件）",
								"remark": 20,
								"price": 56,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jg_jgjzxx.jpg"
							},
							{
								"name": "土木工程测量",
								"remark": 20,
								"price": 56,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jg_tmgccl.jpg"
							},
							{
								"name": "运筹学(第4版)(本科版)",
								"remark": 20,
								"price": 56,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jg_ycx.jpg"
							},
				
						]
					}, {
						"id": 2,
						"name": "信息自动化学院",
						"foods": [{
								"name": "毛泽东思想和中国特色社会主义理论体系概论（2021年版） ",
								"remark": 20,
								"price": 25,
								"imageUrl": "https://img14.360buyimg.com/pop/jfs/t1/184033/39/21231/68054/612b1c6eE48d84278/3e0f3d30986b88ef.jpg"
							},
							{
								"name": "计算机网络",
								"remark": 20,
								"price": 59.80,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/xz_jsjwl.jpg"
							},
							{
								"name": "机器学习从原理到应用",
								"remark": 20,
								"price": 55.00,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/xz_jqxx.jpg"
							},
							{
								"name": "信号与线性系统分析(第5版)",
								"remark": 20,
								"price": 56.00,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/xz_xhyxxxtfx.jpg"
							},
							{
								"name": "自动控制原理(第七版)",
								"remark": 20,
								"price": 89.80,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/xz_zdkzyl.jpg"
							},
							{
								"name": "运筹学基础及应用(第六版)",
								"remark": 20,
								"price": 49.80,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/xz_ycx.jpg"
							},
							{
								"name": "工业工程专业新形态系列教材工程经济学(第五版)",
								"remark": 20,
								"price": 52.00,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/xz_gcjjx.jpg"
							},
							{
								"name": "模拟电子技术基础（第五版）",
								"remark": 20,
								"price": 59.90,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/xz_mndzjsjc.jpg"
							},
						]
					}, {
						"id": 3,
						"name": "电力院",
						"foods": [{
							"name": "毛泽东思想和中国特色社会主义理论体系概论（2021年版）",
							"remark": 20,
							"price": 12,
							"imageUrl": "https://img14.360buyimg.com/pop/jfs/t1/184033/39/21231/68054/612b1c6eE48d84278/3e0f3d30986b88ef.jpg"
						}]
					}, {
						"id": 4,
						"name": "机电院",
						"foods": [{
								"name": "机械原理(第九版)",
								"remark": 20,
								"price": 53,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jd_jxyl.jpg"
							},
							{
								"name": "毛泽东思想和中国特色社会主义理论体系概论(2021年)",
								"remark": 20,
								"price": 25,
								"imageUrl": "https://img14.360buyimg.com/pop/jfs/t1/184033/39/21231/68054/612b1c6eE48d84278/3e0f3d30986b88ef.jpg"
							},
							{
								"name": "工程流体力学(第四版)",
								"remark": 20,
								"price": 12,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jd_gcltlx.jpg"
							},
							{
								"name": "普通化学",
								"remark": 20,
								"price": 49.8,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jd_pthx.jpg"
							},
							{
								"name": "材料力学(I)(第6版)",
								"remark": 20,
								"price": 52,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jd_cllx11.jpg"
							},
							{
								"name": "材料力学II(第6版)",
								"remark": 20,
								"price": 52,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jd_cllx2.jpg"
							},
							{
								"name": "电工学(少学时)(第五版)",
								"remark": 20,
								"price": 54,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jd_dgx.jpg"
							},
							{
								"name": "高等学校教材大学化学实验",
								"remark": 20,
								"price": 26.4,
								"imageUrl": "cloud://booktooneway-9goh81vsda254923.626f-booktooneway-9goh81vsda254923-1312317548/static/books/imgs/jd_dxhxsy.jpg"
							},
						]
					}, {
						"id": 5,
						"name": "法学院",
						"foods": [{
							"name": "毛泽东思想和中国特色社会主义理论体系概论（2021年版）1",
							"remark": 20,
							"price": 12,
							"imageUrl": "https://img14.360buyimg.com/pop/jfs/t1/184033/39/21231/68054/612b1c6eE48d84278/3e0f3d30986b88ef.jpg"
						}]
					}, {
						"id": 6,
						"name": "艺传院",
						"foods": [{
							"name": "毛泽东思想和中国特色社会主义理论体系概论（2021年版）2",
							"remark": 20,
							"price": 12,
							"imageUrl": "https://img14.360buyimg.com/pop/jfs/t1/184033/39/21231/68054/612b1c6eE48d84278/3e0f3d30986b88ef.jpg"
						}]
					}, {
						"id": 7,
						"name": "农工院",
						"foods": [{
								"name": "毛泽东思想和中国特色社会主义理论体系概论（2021年版）3",
								"remark": 1,
								"price": 12,
								"imageUrl": "https://img14.360buyimg.com/pop/jfs/t1/184033/39/21231/68054/612b1c6eE48d84278/3e0f3d30986b88ef.jpg"
							},
							{
								"name": "毛泽东思想和中国特色社会主义理论体系概论（2021年版）4",
								"remark": 20,
								"price": 12,
								"imageUrl": "https://img14.360buyimg.com/pop/jfs/t1/184033/39/21231/68054/612b1c6eE48d84278/3e0f3d30986b88ef.jpg"
							},
				
						]
					}, {
						"id": 8,
						"name": "建筑院",
						"foods": [{
							"name": "毛泽东思想和中国特色社会主义理论体系概论（2021年版）5",
							"remark": 20,
							"price": 12,
							"imageUrl": "https://img14.360buyimg.com/pop/jfs/t1/184033/39/21231/68054/612b1c6eE48d84278/3e0f3d30986b88ef.jpg"
						}]
					},
				
				
				]
				
			}

		},
		components: {
			shopcart,
			cartcontrol
		},
		onLoad(e) {
			// console.log("goods")
			// console.log(goods)
			// this.goods = goods;
			
			// this.goods = goods.data().goods;
			// wx.cloud.init({
			// 	env: "booktooneway-9goh81vsda254923"
			// })
			
			this.mealType = parseInt(e.mealType) + 1
			// console.log(this.mealType + 1)
			// // this.getMenu(1);
			// console.log(goods.data().goods)
			this.windows_height = Number(uni.getSystemInfoSync().windowHeight) - 55;
			setTimeout(() => {
				this.getHeightList();
			}, 1000)
			
			
		},

		computed: {
			getList() {
				let result = [];
				this.goods.forEach((good) => {

					good.foods.forEach((food) => {

						if (food.count) {
							result.push(food)
						}
					})
				})
				return result

			},
		},
		methods: {
			// 点击侧边栏
			select(index) {
				this.currentIndex = index;
				this.setScrollH(index);
			},
			getMenu(typeId) {
				if (typeId == 9) {
					uni.hideLoading()
					return;
				}
				uni.showLoading({
					title: "正在加载菜单"
				})
				var that = this
				// for (var i in that.goods) {
				// var typeId = that.goods[i].id
				console.log("当前id：", typeId)
				uni.request({
					url: 'http://lyuanzhi.com:8090' + '/canteen/getMenuListByType',
					method: 'POST',
					data: {
						mealType: that.mealType,
						type: typeId
					},
					header: {
						'content-type': 'application/x-www-form-urlencoded'
					},
					success: res => {
						console.log(res)
						if (res.statusCode == 200) {
							var resData = res.data.data
							for (var h in resData) {
								var id = parseInt(typeId)
								console.log("返回的数据：", id, resData[h].type)
								if (resData[h].type == id) {
									that.goods[id - 1].foods.push(resData[h])
								}
							}
						}
					},
					fail: res => {
						console.log(res)
					}
				})
				// }
				return this.getMenu(typeId + 1)
			},
			// 设置点击侧边栏右边滚动的高度
			setScrollH: function(index) {
				var that = this;
				let height = 0;
				var query = uni.createSelectorQuery();
				let foods = query.selectAll('.foods');

				this.$nextTick(function() {
					foods.fields({
						size: true
					}, data => {
						if (index == 0) {
							that.foodSTop = 0;
						}
						for (let i = 0; i < index; i++) {

							height += parseInt(data[i].height);
							// console.log('fh', foods);
							that.foodSTop = height;
							// console.log(that.foodSTop)
						}

					}).exec();
				})

			},

			addCart: function(item) {
				if (item.count >= 0) {
					item.count++
					this.goods.forEach((good) => {
						good.foods.forEach((food) => {
							// 根据名字添加购物车,实际环境根据需要更改
							if (item.name == food.name)
								food.count = item.count
						})
					})
				} else {
					console.log('add')
					this.goods.forEach((good) => {
						good.foods.forEach((food) => {
							if (item.name == food.name)
								Vue.set(food, 'count', 1)
						})
					})
				}
			},
			decreaseCart(item) {
				if (item.count) {
					item.count--
					this.goods.forEach((good) => {
						good.foods.forEach((food) => {
							if (item.name == food.name)
								food.count = item.count
						})
					})
				}
			},
			// 清空购物车
			delAll() {
				this.goods.forEach((good) => {
					good.foods.forEach((food) => {
						if (food.count) {
							food.count = 0
						}
					})
				})
			},
			getHeightList() {
				let _this = this;
				let selectorQuery = uni.createSelectorQuery().in(this);
				selectorQuery.select('.left-content').boundingClientRect(function(rects) {
					_this.left_height = rects.height;
				});
				selectorQuery.selectAll('.foods').boundingClientRect(function(rects) {
					_this.right_height = rects.map((item) => item.top);
				}).exec();
			},
			myscroll(e) {
				//引入节流	
				let right_content_height = e.detail.scrollHeight - this.windows_height;
				if (right_content_height == e.detail.scrollTop) {
					return;
				}
				let scroll_top = e.detail.scrollTop + 110; //110是banner图的高度
				//判断当前的scrollTop在哪个区间内;
				let now = +new Date();
				if (now - this.last > 100) {
					this.last = now;
					let active_index = this.right_height.findIndex((value, index, arr) => value <= scroll_top &&
						scroll_top <
						arr[
							index + 1]);
					this.currentIndex = active_index;
					if (this.left_height - this.windows_height) {
						//如果有超出部分
						let diff = this.left_height - this.windows_height
						this.left_scroll = Math.round((active_index * diff) / (this.goods.length - 1))
					}
				}
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		position: absolute;
		top: 0;
		bottom: 55px;
		width: 100%;
		overflow: hidden;
	}

	.current {
		position: relative;
		z-index: 0;
		background-color: #fff;
		color: #00A0DC;
		border-left: 5px solid #00A0DC;
	}

	.menu-wrapper {
		text-align: center;
		width: 22%;
		display: flex;
		flex-direction: column;
		background: #f3f5f7;

	}

	.menu-item {
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
		height: 50px;
	}

	.allcount {
		position: absolute;
		right: 6px;
		top: 8px;
		display: inline-block;
		padding: 0 4px;
		font-size: 9px;
		line-height: 16px;
		font-weight: 400;
		border-radius: 50%;
		background-color: #f01414;
		color: #ffffff;
	}

	.foods-wrapper {
		margin-left: 4px;
		width: 78%;
	}

	.food,
	.food-btm,
	.content {
		display: flex;
		flex-direction: row;
	}

	.food-title {
		padding: 2px 0;
		font-size: 40upx;
		/* border-bottom: solid 2upx #777777; */
	}

	.food-info {
		margin-left: 10px;
		margin-right: 16px;
		display: flex;
		flex-direction: column;
		flex: 2;
	}

	.food-btm {
		justify-content: space-between;
	}

	.food-price {
		color: #f01414;
		font-size: 16px;
	}
</style>
