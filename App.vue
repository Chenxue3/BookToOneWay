<script>
	export default {
		onLaunch: function() {
			
			wx.cloud.init({
				env: "booktooneway-9goh81vsda254923"
			})
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
	/*每个页面公共css */
	 @import url("/static/iconfont.css")
</style>
