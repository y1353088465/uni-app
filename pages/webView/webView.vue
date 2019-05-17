<template>
	<view class="web_box">
		<view class="status_bar">
			<view class="top_view"></view>
		</view>
		<div class="banner">
			<p>〈</p>
			<p></p>
			<p></p>
		</div>
		<web-view class="web_view" :webview-styles="webviewStyles" :src="src"></web-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				src: "",
				webviewStyles: {
					progress: false
				}
			};
		},
		mounted() {
			uni.getStorage({
				key: 'sao_url',
				success: (res) => {
					console.log(JSON.stringify(res))
					this.src = res.data.result
				},
				fail: () => {

				}
			});

		}
	}
</script>

<style lang="scss">
	.status_bar {
		height: var(--status-bar-height);
		width: 100%;
		background-color: #F8F8F8;
	}

	.top_view {
		height: var(--status-bar-height);
		width: 100%;
		position: fixed;
		background-color: #000;
		top: 0;
		z-index: 999;
	}
	.web_box{
		width:100%;
		height:100vh;
		overflow: hidden;
		.banner{
			width:100%;
			height:120upx;
			display: flex;
			justify-content: space-between;
			flex-direction: row;
		}
		.web_view{
			flex:1;
			overflow-y: scroll;
		}
	}
</style>
