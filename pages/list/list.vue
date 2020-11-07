<template>
	<view class="container">
		<scroll-view class="leftnav" scroll-y scroll-anchoring>
			<view v-for="(item,index) in navbar" :key="item.cat_id" :class="['item',active===index?'active':'']" 
			@click="leftclick(index,item.cat_name)">
				{{item.cat_name}}
			</view>
		</scroll-view>
		<scroll-view class="rightinfo" scroll-y>
			<view class="info" v-for="(item,index) in rightinfo" :key="index">
				{{item.goods_name}}
			</view>
			<view class="msg" v-if="rightinfo.length === 0">暂无数据</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navbar:[],
				rightinfo:[],
				active:0,
			}
		},
		onLoad() {
			this.getlist()
			console.log(this.navbar);
		},
		methods:{
			getlist(){
				let that = this
				uni.request({
					url:'https://api-hmugo-web.itheima.net/api/public/v1/categories',
					success(res) {
						if(res.statusCode == 200){
							that.navbar = res.data.message
							that.leftclick(0,that.navbar[0].cat_name);
						}
					}
				})
				
			},
			leftclick(index,name){
				this.active = index;
				let that = this;
				uni.request({
					url:'https://api-hmugo-web.itheima.net/api/public/v1/goods/qsearch?query='+name,
					success(res) {
						if(res.statusCode == 200){
							that.rightinfo = res.data.message
							console.log(that.rightinfo);
						}
					}
				})
			}
		},
	}
</script>

<style scoped>
	page{
		height: 100%;
		overflow: hidden;
	}
	.container{
		height: 100%;
		display: flex;
		justify-content: space-between;
	}
	
	.leftnav{
		width: 200rpx;
		height: 100%;
		margin-right: 20rpx;
	}
	.rightinfo{
		width: 555rpx;
		height: 100%;
		box-sizing: border-box;
		padding: 10rpx;
	}
	.rightinfo .info{
		line-height: 60rpx;
		text-indent: 24rpx;
		margin-bottom: 20rpx;
	}
	.item{
		width: 100%;
		height: 100rpx;
		line-height: 100rpx;
		text-align: center;
		font-size: 32rpx;
	}
	.active{
		background-color: #007AFF;
		color: #fff;
	}
	.msg{
		width: 100%;
		line-height: 300rpx;
		text-align: center;
	}
</style>
