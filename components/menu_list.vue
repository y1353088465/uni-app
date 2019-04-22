<template>
	<view>
		<div @click="hide()" class="fog"></div>
		<div class="sanjiao"></div>
		<ul class="menu_fog">
			<li>
				<span class="iconfont">&#xe715;</span>
				<text>发起群聊</text>
			</li>
			<li>
				<span class="iconfont">&#xe61e;</span>
				<text>添加朋友</text>
			</li>
			<li @click="sao()">
				<span class="iconfont">&#xe680;</span>
				<text>扫一扫</text>
			</li>
			<li>
				<span class="iconfont">&#xe6c4;</span>
				<text>收付款</text>
			</li>
			<li>
				<span class="iconfont">&#xe621;</span>
				<text>帮助与反馈</text>
			</li>
		</ul>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				menu_components: false,
			};
		},
		methods: {
			hide() {
				this.$emit("menu_hide", this.menu_components);
			},
			sao() {
				uni.scanCode({
					success: function(res) {
						alert(JSON.stringify(res))
					}
				});
			}
		}
	}
</script>

<style lang="scss">
	.fog {
		z-index: 1;
		position: absolute;
		right: 0;
		top: 0;
		width: 100%;
		height: 100vh;
	}

	.sanjiao {
		position: absolute;
		right: 45upx;
		top: 90upx;
		width: 25upx;
		height: 25upx;
		border-radius: 3upx;
		background: #5a5a5a;
		transform: rotate(45deg);
		z-index: 2;
	}

	.menu_fog {
		position: absolute;
		right: 15upx;
		top: 100upx;
		background: #5a5a5a;
		border-radius: 10upx;
		padding-left: 20upx;
		color: #fff;
		z-index: 2;

		li {
			display: flex;
			flex-direction: row;
			align-items: center;
			height: 91upx;
			width: 280upx;
			letter-spacing: 3upx;

			span {
				margin: 0 20upx 0 15upx;
			}

			text {
				font-size: 30upx;
				flex: 1;
				line-height: 70upx;
				border-bottom: 1upx solid #666;
				text-align: left;
			}
		}
	}
</style>
