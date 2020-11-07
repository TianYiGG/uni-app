<template>
	<view>
		<view class="list">
			<view class="list-item" v-for="(item,index) in datas" :key='index' @click="godetails(item.goods_id)">
				<view class="list-img">
					<image :src="item.goods_big_logo" mode="aspectFit"></image>
				</view>
				<view>
					<text class="list-title">{{item.goods_name}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item:'',
				datas:[],
				placeholderImage:'../static/image/timg.jpg',//占位图
			};
		},
		methods:{
			getGoodsinfo(){
				let that = this;
				uni.request({
					url:'https://api-hmugo-web.itheima.net/api/public/v1/goods/search?query='+this.item,
					success(res) {
						if(res.statusCode == 200){
							that.datas = res.data.message.goods
							console.log(typeof(that.datas))
							for(let x in that.datas){
								console.log(that.datas[x]);
								if(that.datas[x].goods_big_logo == ""){
									that.datas[x].goods_big_logo = that.placeholderImage
								}
							}
						}
					}
				})
			},
			godetails(id){
				uni.navigateTo({
					url:'/pages/details/details?goods_id='+id
				})
			}
		},
		onLoad(option) {
			console.log(option)
			this.item = option.query
			this.getGoodsinfo();
		}
	}
</script>

<style scoped>
	.list {
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
		box-sizing: border-box;
		padding: 20rpx;
	}
	
	.list-item {
		width: 49%;
		margin-bottom: 20rpx;
	}
	
	.list-item image {
		width: 100%;
		height: 272rpx;
	}
	
	.list-img {
		font-size: 0;
	}
	
	.list-title {
		margin-bottom: 10rpx;
		font-size: 30rpx;
		line-height: 40rpx;
		padding-left: 10rpx;
	}
</style>
