<template>
	<view>
		<div class="header">
			<text>{{msg}}</text>
			<div class="iconbox">
				<span @click="search_msg()" class="iconfont">&#xe609;</span>
				<span @click="more_menu_page()" class="iconfont">&#xe62f;</span>
			</div>
		</div>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				menu_status: false,
			};
		},
		props: ["msg"],
		methods: {
			search_msg() {
				uni.navigateTo({
					url: '/pages/index/wx_search/wx_search',
					animationType: 'pop-in',
					animationDuration: 400,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			},
			more_menu_page() {
				this.menu_status = true;
				this.$emit("menu_status", this.menu_status);
			}
		}
	}
</script>

<style lang="scss">
	.header {
		height: 90upx;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-content: center;
		padding: 0 25upx;
		background: #f1f5f9;

		text {
			font-size: 30upx;
			line-height: 90upx;
		}

		.iconbox {
			display: flex;
			flex-direction: row;
			align-items: center;

			span {
				font-size: 40upx;
			}

			span:nth-child(1) {
				margin-right: 45upx;
				font-size: 45upx;
			}
		}
	}
</style>
