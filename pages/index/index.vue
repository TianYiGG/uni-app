<template>
	<view class="content">
		<swiper class="swiper" indicator-dots autoplay :indicator-color="indicatorColor" :indicator-active-color='color'>
			<swiper-item v-for="item in swipers" :key="item.goods_id">
				<image :src="item.image_src"></image>
			</swiper-item>
		</swiper>
		<view class="home-nav">
			<view v-for="(item,index) in nav" :key='index' @click="link(item.url)">
				<image :src="item.img_url"></image>
			</view>
		</view>
		<view>
			<view class="list-pic">
				<view>
					<image src="../../static/image/list-pic2.png"></image>
				</view>
			</view>
			<goods-list :list="list[0]" @godetails="godetails"></goods-list>
		</view>
		<view>
			<view class="list-pic">
				<view>
					<image src="../../static/image/list-pic1.png"></image>
				</view>
			</view>
			<goods-list :list="list[1]" @godetails="godetails"></goods-list>
		</view>
		<view>
			<view class="list-pic">
				<view>
					<image src="../../static/image/list-pic3.png"></image>
				</view>
			</view>
			<goods-list :list="list[2]" @godetails="godetails"></goods-list>
		</view>
	</view>
</template>

<script>
	import goodList from '../../components/good-list.vue';
	export default {
		data() {
			return {
				indicatorColor: '#fff',
				color: 'blue',
				swipers: [],
				nav: [{
						img_url: '../../static/image/icon1.png',
						url: '/pages/list/list'
					},
					{
						img_url: '../../static/image/icon2.png',
						url: '/pages/list/list'
					},
					{
						img_url: '../../static/image/icon3.png',
						url: '/pages/list/list'
					},
					{
						img_url: '../../static/image/icon4.png',
						url: '/pages/list/list'
					},
				],
				list:[],//产品
			}
		},
		onLoad() {
			this.getswiper()
			this.getlist()
		},
		methods: {
			getswiper() {
				let that = this;
				uni.request({
					url: 'https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata',
					success(res) {
						if (res.statusCode == 200) {
							that.swipers = res.data.message
						}
						// console.log(res);
					}
				})
			},
			getlist(){
				let that = this;
				uni.request({
					url:'https://api-hmugo-web.itheima.net/api/public/v1/home/floordata',
					success(res) {
						if (res.statusCode == 200) {
							let list = [];
							for(let i of res.data.message){
								list.push(i.product_list.slice(1));
							}
							that.list = list;
						}
					}
				})
			},
			godetails(url){
				console.log(url)
				uni.navigateTo({
					url
				})
			},
			link(url) {
				uni.reLaunch({
				    url
				});
			}
		},
		components: {
			"goods-list":goodList
		}
	}
</script>

<style>
	.swiper {
		width: 750rpx;
		height: 380rpx;
	}

	.swiper image {
		width: 100%;
		height: 100%;
	}

	.home-nav {
		width: 750rpx;
		height: 240rpx;
		box-sizing: border-box;
		padding: 20rpx;
		display: flex;
		justify-content: space-between;
		flex-wrap: nowrap;
	}

	.home-nav view {
		width: 25%;
		height: 120rxp;
	}

	.home-nav view image {
		width: 100%;
		height: 100%;
	}
	.list-pic {
		width: 750rpx;
		margin: 20rpx 0;
	}
	
	.list-pic image {
		width: 750rpx;
		height: 58rpx;
	}
	
</style>
