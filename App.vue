<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>
<style>
	/* #ifdef MP-WEIXIN*/
	page {
		height: 100%;
	}
	/* #endif */
	/*每个页面公共css */
</style>
