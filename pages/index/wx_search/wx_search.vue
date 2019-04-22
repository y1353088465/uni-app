<template>
	<view class="search">
		<view class="status_bar">
			<view class="top_view"></view>
		</view>
		<div class="header">
			<img @click="go_back()" src="../../../static/img/header_back.png" alt="">
			<input focus="true" placeholder="搜索" placeholder-style="color:#aeaeae;font-size:30upx;letter-spacing:5upx;" type="text">
		</div>
		<div class="tips">
			<p class="tips_tit">搜索指定内容</p>
			<ul>
				<li>朋友圈</li>
				<li>文章</li>
				<li>公众号</li>
			</ul>
			<ul>
				<li>小程序</li>
				<li>音乐</li>
				<li>表情</li>
			</ul>
		</div>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		},
		methods: {
			go_back() {
				uni.navigateBack({
					delta: 1,
					animationType: 'pop-out',
					animationDuration: 400
				});
			}
		}
	}
</script>

<style lang="scss">
	.search {
		background: #fafafa;
		height: 100vh;

		.status_bar {
			height: var(--status-bar-height);
			width: 100%;
			background-color: #F8F8F8;
		}

		.top_view {
			height: var(--status-bar-height);
			width: 100%;
			position: fixed;
			background-color: #F8F8F8;
			top: 0;
			z-index: 999;
		}

		.tips {
			.tips_tit {
				line-height: 110upx;
				text-align: center;
				font-size: 30upx;
				color: #aeaeae;
			}

			ul {
				display: flex;
				padding: 0 40upx;
				flex-direction: row;
				align-items: center;
				height: 90upx;

				li {
					flex: 1;
					text-align: center;
					border-right: 1px solid #dedede;
					font-size: 28upx;
					color: #235789;
					line-height: 28upx;
				}

				li:last-child {
					border: none;
				}
			}
		}
	}

	.header {
		width: 100%;
		display: flex;
		flex-direction: row;
		height: 90upx;
		align-items: center;
		border-bottom: 1px solid #eee;

		img {
			width: 18upx;
			height: 32upx;
			padding: 0 25upx;
		}

		input {
			flex: 1;
			height: 60upx;
			font-size: 30upx;
			border: none;
			margin-top: 3upx;
			caret-color: orange;
		}

		input::-webkit-input-placeholder {
			font-size: 30px;
			color: #fff;
		}

	}
</style>
