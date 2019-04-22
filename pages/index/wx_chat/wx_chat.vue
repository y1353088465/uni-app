<template>
	<view class="wx_chat">
		<IndexHeader v-on:menu_status="menu_status" msg="微微信"></IndexHeader>
		<div class="scroll-Y">
			<view @click="chat_with_friend()" v-for="i in chat_list" id="demo1" class="scroll-view-item uni-bg-red">
				<img src="../../../static/logo.png" alt="">
				<ul class="text_box">
					<li class="title_txt">
						<text>{{i.title}}</text>
						<text>{{i.time}}</text>
					</li>
					<li class="msg_txt">
						<text></text>
						<text>{{i.text}}</text>
					</li>
				</ul>
			</view>
		</div>
		<MenuList v-on:menu_hide="menu_hide" v-if="menu_list_status"></MenuList>
	</view>
</template>

<script>
	import IndexHeader from "../../../components/index_header.vue"
	import MenuList from "../../../components/menu_list.vue"
	export default {
		data() {
			return {
				scrollTop: 0,
				old: {
					scrollTop: 0
				},
				chat_list: [{
					title:"大型公共聊天室",
					text:"websocket",
					time:"13.01"
				},
				 {
				 	title:"同服务器交流群",
				 	text:"进入de聊天室是相同的一个",
				 	time:"13.08"
				 }, ],
				menu_list_status: false,
			};
		},
		components: {
			IndexHeader,
			MenuList
		},
		methods: {
			//监听子元素事件传输值
			menu_status(value) {
				this.menu_list_status = value;
			},
			menu_hide(value) {
				this.menu_list_status = value;
			},
			chat_with_friend() {
				uni.navigateTo({
					url: '/pages/next/next',
					animationType: 'pop-in',
					animationDuration: 400,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style scoped lang="scss">
	.wx_chat {
		flex: 1;
		display: flex;
		flex-direction: column;
		position: relative;

		.scroll-Y {
			flex: 1;
			overflow: scroll;

			.scroll-view-item {
				height: 115upx;
				display: flex;
				flex-direction: row;
				align-items: center;
				margin-top: 5upx;

				img {
					height: 90upx;
					width: 90upx;
					padding: 30upx;
				}

				.text_box {
					flex: 1;
					border-bottom: 1upx solid #ccc;
					height: 100%;
					display: flex;
					flex-direction: column;
					text-align: left;

					li {
						padding: 0;
					}

					.title_txt {
						display: flex;
						flex-direction: row;
						justify-content: space-between;
						padding-top: 10upx;

						text:first-child {
							font-size: 30upx;
						}

						text:last-child {
							font-size: 26upx;
							color: #999;
							margin-right: 30upx;
						}
					}

					.msg_txt {
						display: flex;
						flex-direction: row;
						font-size: 26upx;
						color: #555;
						padding-top: 15upx;
					}
				}
			}


		}

	}
</style>
