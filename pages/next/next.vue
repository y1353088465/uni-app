<template>
	<view class="chat_page">
		<view class="status_bar">
			<view class="top_view"></view>
		</view>
		<view class="header">
			<p @click="go_back()">返回</p>
			<p>与xxx的聊天</p>
			<p></p>
		</view>
		<view class="chat_history">
			<view v-for="i in data_list">
				<p v-if='i.text'>{{i.name}}： {{i.text}}</p>
				<p v-if='!i.text'>{{i.name}}加入聊天室</p>
			</view>
		</view>
		<view class="input_box">
			<input id="inp_box" v-model="obj.inp_msg" type="text">
			<p class="send_msg" id="send_btn" @mousedown="send($event)" @click="send_msg($event)">发送</p>
		</view>
		<!-- 		<div v-if="fog_status" class="set_name">
			<input placeholder="请输入您在此聊天室的昵称" v-model="obj.user_name" Focus type="text">
			<p @click="set_name_ok">确定</p>
		</div>
		<Fog :fog_status="fog_status"></Fog> -->
	</view>
</template>

<script>
	// import Fog from "../../components/fog.vue"
	export default {
		data() {
			return {
				data_list: [],
				socketOpenStatus: false,
				// fog_status: true,
				obj: {
					user_name: "",
					inp_msg: "",
				},
				ws: null
			};
		},
		components: {
			// Fog
		},
		watch: {
			obj() {
				console.log(11000)
			}
		},
		mounted() {

			uni.getStorage({
				key: 'user_name',
				success: (res) => {
					if (res.data) {
						this.obj.user_name = res.data;
						// 新建websocket
						this.socketConnect()
						this.socketOpen()
						this.socketClose()
						this.socketError()
						this.socketMessage()
					}else{
						uni.navigateTo({
							url: '/pages/login/login',
							animationType: 'pop-in',
							animationDuration: 400,
							success: res => {},
							fail: () => {},
							complete: () => {}
						});
					}
				}
			});



		},
		beforeDestroy() {
			uni.removeStorage({
				key: 'obj',
				success: function(res) {
					console.log('success');
				}
			});
		},
		methods: {
			// websocket-----------------------------------------------
			socketConnect() {
				uni.connectSocket({
					url: 'ws://192.168.118.140:8001',
				});
			},
			socketOpen() {
				uni.onSocketOpen((res) => {
					this.socketOpenStatus = true
					console.log('WebSocket连接已打开！');
					this.sendSocketMessage(JSON.stringify(this.obj))
				});
			},
			sendSocketMessage(msg) {
				if (this.socketOpenStatus) {
					uni.sendSocketMessage({
						data: msg
					});
				} else {
					socketMsgQueue.push(msg);
				}
			},
			socketClose() {
				uni.onSocketClose((res) => {
					console.log('WebSocket 已关闭！');
				});
			},
			socketError() {
				uni.onSocketError((res) => {
					console.log('WebSocket连接打开失败，请检查！');
				});
			},
			socketMessage() {
				uni.onSocketMessage((e) => {
					if (e.data !== "success") {
						this.data_list.push(JSON.parse(e.data))
					}
					console.log('收到服务器内容：' + e.data);
				});
			},
			// websocket--------------------------------------------------------

			go_back() {
				uni.navigateBack({
					delta: 1
				});
			},
			send(e) {
				let inp = document.getElementById("send_btn");
				inp.focus()
				// 				e.preventDefault();
				// 				e.stopPropagation();
				// 				e.cancelBubble = true;
				if (e && e.preventDefault)
					e.preventDefault();
				//IE阻止默认事件
				else
					window.event.returnValue = false;
				return false;
			},
			send_msg(e) {
				if (this.obj.inp_msg) {
					this.sendSocketMessage(JSON.stringify(this.obj))
					this.obj.inp_msg = '';
				}
			},

		}
	}
</script>

<style scoped lang="scss">
	.chat_page {
		width: 100%;
		height: 100vh;
		display: flex;
		flex-direction: column;
		position: relative;

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

		.set_name {
			position: absolute;
			left: 50%;
			top: 50%;
			transform: translate(-50%, -50%);
			background: #fff;
			border-radius: 10upx;
			overflow: hidden;
			padding: 30upx;
			box-shadow: 0upx 0upx 15upx #666;
			z-index: 2;

			input {
				width: 500upx;
				height: 80upx;
				border-bottom: 1px solid #ccc;
			}

			p {
				width: 100%;
				line-height: 80upx;
				background: #59ef79;
				color: #fff;
				text-align: center;
				margin-top: 25upx;
				border-radius: 7upx;
			}
		}

		.header {
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			padding: 0 20upx;
			height: 90upx;
			align-items: center;
			border-bottom: 1px solid #eee;
			background: #eee;

			p {
				width: 80upx;
				font-size: 28upx;
			}

			p:nth-child(2) {
				flex: 1;
				text-align: center;
				font-size: 30upx;
			}
		}

		.chat_history {
			flex: 1;
			overflow-y: scroll;
			padding: 0 20upx;
			line-height: 60upx;
			background: #fff;

			p {
				font-size: 28upx;
			}
		}

		.input_box {
			display: flex;
			flex-direction: row;
			height: 100upx;
			align-items: center;
			background: #eee;
			padding: 0 20upx;

			input {
				flex: 1;
				border: 1px solid #eee;
				background: #fff;
				height: 60upx;
				border-radius: 10upx;
			}

			p {
				width: 150upx;
				height: 60upx;
				background: #efefef;
				text-align: center;
				line-height: 60upx;
				font-size: 28upx;
				background: #59ef79;
				border-radius: 10upx;
				margin-left: 10upx;
			}
		}
	}
</style>
