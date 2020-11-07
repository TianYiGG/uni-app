<template>
	<view>
		<view class="list">
			<view class="list-item" v-for="(item,index) in list" :key='index' @click="godetails(item.navigator_url)">
				<view class="list-img">
					<image :src="item.image_src" mode="aspectFit"></image>
				</view>
				<view>
					<text class="list-title">{{item.name}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods:{
			godetails(url){
				this.$emit('godetails',url)
			}
		},
		props:[
			'list'
		]
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
		margin-bottom: 10rpx;
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
