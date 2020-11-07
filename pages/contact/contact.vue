<template>
	<view class="contact">
		<view class="header">
			<image :src="header" mode=""></image>
		</view>
		<!-- <text class="login" @click="auth">点击登录</text> -->
		<!-- #ifdef MP-WEIXIN -->
		<view>
			<button hover-class="none" v-if="nickName" open-type="getUserInfo" @getuserinfo="getUserInfo">登录</button>
			<view class="username" v-else='nickName'>{{userInfo.nickName}}</view>
		</view>
		<!-- #endif -->
	</view>
</template>
<script>
	export default {
		data() {
			return {
				header: '../../static/image/header.jpg',
				userInfo:{},
				nickName:true,
			}
		},
		onLoad() {

		},
		methods: {
			getUserInfo() {
				// 授权登录
				uni.getUserInfo({
					success: (res) => {
						this.userInfo = res.userInfo;
						this.header = res.userInfo.avatarUrl;
						this.nickName = false;
					},
					fail: () => {
						console.log("未授权");
					}
				})
			}
		}
	}
</script>

<style scoped>
	.contact {
		height: 100%;
		overflow: hidden;
	}

	.header {
		width: 200rpx;
		height: 200rpx;
		border-radius: 50%;
		overflow: hidden;
		margin: 100rpx auto 20rpx;
	}

	.header image {
		width: 100%;
		height: 100%;
	}

	.login {
		display: block;
		text-align: center;
	}

	button::after{
		border: none;
		background-color: none;
	}
	.username{
		text-align: center;
		line-height: 40rpx;
		margin: 20rpx 0;
	}
</style>
