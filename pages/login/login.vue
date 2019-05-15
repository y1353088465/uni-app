<template>
	<view class="login">
		<p class="title">微 微 信</p>
		<div class="login_box">
			<input v-model="user_name" placeholder-style="font-size: 14px;text-align:center;color:#01D867;" placeholder="请输入您在本软件的昵称"
			 class="user_name" type="text" />
			<p @click="login_in()" class="login_btn">登 陆</p>
			<p class="tips">作为您在本产品的唯一身份证明,昵称为必填选项</p>
		</div>
		<p></p>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				user_name: '',
			};
		},
		methods: {
			login_in() {
				if (this.user_name) {
					uni.setStorage({
						key: 'user_name',
						data: this.user_name,
						success: (res) => {
							this.send_info();

							console.log(JSON.stringify(res));

						},
						error: (err) => {
							console.log(err)
						}
					});
				}
			},
			send_info() {
				console.log("发送请求")

				uni.request({
					url: 'http://192.168.118.140:1100/login_in', //仅为示例，并非真实接口地址。
					method: 'GET',
					data: {
						phone: this.user_name
					},
					header: {
						"Content-Type": 'application/json',
					},
					success: (data) => {
						console.log(data);
						if (data.data.data.status) {
							uni.navigateTo({
								url: '/pages/index/index',
								animationType: 'pop-in',
								animationDuration: 400,
								success: res => {},
								fail: () => {},
								complete: () => {}
							});
						} else {
							alert(data.data.data.data)
							uni.showToast({
								title: data.data.data.data,
								icon:false,
								duration: 2000
							});
						}

					},
					fail: (err) => {
						console.log(JSON.stringify(err))
					}
				});
			}
		},
		mounted() {
			uni.getStorage({
				key: 'user_name',
				success: (res) => {
					uni.navigateTo({
						url: '/pages/index/index',
						animationType: 'pop-in',
						animationDuration: 400,
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
					console.log(res);
				},
				fail: (res) => {

					console.log(JSON.stringify(res))
				}
			});
		},
		beforeDestroy() {
			uni.getStorage({
				key: 'user_name',
				success: (res) => {
					uni.navigateTo({
						url: '/pages/index/index',
						animationType: 'pop-in',
						animationDuration: 400,
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
					console.log(res);
				},
				fail: (res) => {
					uni.navigateTo({
						url: '/pages/login/login',
						animationType: 'pop-in',
						animationDuration: 400,
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
					console.log(res)
				}
			});
		}
	}
</script>

<style scoped lang="scss">
	.login {
		width: 100%;
		height: 100vh;
		min-height: 1000upx;
		background: linear-gradient(left top, #2468ac 10%, rgba(0, 0, 0, .8) 50%, #789ac9 100%);
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center;

		.user_name::-webkit-input-placeholder {
			font-size: 26upx;
		}

		.title {
			font-size: 80upx;
			transform: translateY(150upx) skew(-10deg);
			font-weight: 600;
			color: #01D867;
			text-shadow: 10upx 10upx 10upx #7294BF;
			flex-shrink: 0;
		}

		.login_box {
			width: 100%;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			width: 398upx;
			position: relative;
			flex-shrink: 0;

			.user_name {
				border-bottom: 1px solid #01D867;
				width: 100%;
				height: 50upx;
				text-align: center;
				color: #01D867;
			}

			.login_btn {
				text-align: center;
				width: 100%;
				height: 80upx;
				line-height: 80upx;
				margin-top: 150upx;
				// letter-spacing: 10upx;
				border: 1upx solid #01D867;
				border-radius: 50% 0;
				color: #01D867;
			}

			.tips {
				color: orangered;
				font-size: 26upx;
				text-align: center;
				position: absolute;
				width: 398upx;
				left: 0;
				top: 75upx;
			}

		}
	}
</style>
