<template>
	<view>
		<swiper>
			<swiper-item v-for="(item,index) in goodList.pics" :key="index">
				<image :src="item.pics_big" mode=""></image>
			</swiper-item>
		</swiper>
		<view class="goods-info">
			<view class="price">￥{{goodList.goods_price}}</view>
			<view class="goods_name">{{goodList.goods_name}}</view>
			<view class="goodinfo" v-for="(info,index) in goodList.attrs" :key="index">
				<text>{{info.attr_name}} : {{info.attr_vals}}</text>
			</view>
		</view>
		<view class="richtext">
			<rich-text class="rich-text" :nodes="goodList.goods_introduce"></rich-text>
		</view>
		<uni-goods-nav class="cart" :fill="true" :options="options" :buttonGroup="buttonGroup" @click="onClick" @buttonClick="buttonClick" />
	</view>
</template>

<script>
	import uniGoodsNav from '@/components/uni-goods-nav/uni-goods-nav.vue'
	export default {
		data() {
			return {
				goods_id: 0,
				goodList: [],
				options: [{
					icon: 'headphones',
					text: '客服'
				}, {
					icon: 'shop',
					text: '店铺',
					info: 2,
					infoBackgroundColor: '#007aff',
					infoColor: "red"
				}, {
					icon: 'cart',
					text: '购物车',
					info: 2
				}],
				buttonGroup: [{
						text: '加入购物车',
						backgroundColor: '#ff0000',
						color: '#fff'
					},
					{
						text: '立即购买',
						backgroundColor: '#ffa200',
						color: '#fff'
					}
				]
			}
		},
		methods: {
			getGoodsDetails() {
				let that = this;
				uni.request({
					url: 'https://api-hmugo-web.itheima.net/api/public/v1/goods/detail?goods_id=' + that.goods_id,
					success(res) {
						if (res.statusCode == 200) {
							that.goodList = res.data.message;
							console.log(res);
						}
					}
				})
			},
			onClick(e) {
				uni.showToast({
					title: `点击${e.content.text}`,
					icon: 'none'
				})
			},
			buttonClick(e) {
				console.log(e)
				this.options[2].info++
			}
	},
	onLoad(option) {
			this.goods_id = option.goods_id
			this.getGoodsDetails()
		},
		components: {
			uniGoodsNav
		}
	}
</script>

<style scoped>
	swiper {
		width: 750rpx;
		height: 600rpx;
	}

	swiper image {
		width: 100%;
		height: 600rpx;
	}

	.goods-info {
		margin-bottom: 40rpx;
		box-sizing: border-box;
		padding: 20rpx;
		border-bottom: 1px solid #eee;
	}

	text {
		line-height: 80rpx;
	}

	.price {
		color: red;
		font-size: 40rpx;
		font-weight: bold;
		margin: 20rpx 0;
		padding-left: 48rpx;
	}

	.goods_name {
		line-height: 60rpx;
		text-indent: 48rpx;
		letter-spacing: 8rpx;
		margin: 20rpx 0;
	}

	.richtext {
		padding-bottom: 100rpx;
	}
	.cart{
		position: fixed;
		width: 100%;
		bottom: 0;
		left: 0;
		
	}
</style>
