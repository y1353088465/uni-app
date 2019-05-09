<template>
	<view class="content">
		<view class="status_bar">
			<view class="top_view"></view>
		</view>
		<Chat v-if="child_page_num === 0"></Chat>
		<Contacts v-else-if="child_page_num === 1"></Contacts>
		<Find v-else-if="child_page_num === 2"></Find>
		<My :userName="userName" v-else-if="child_page_num === 3"></My>
		<div class="bottom_btn_box">
			<div v-for="(i,j) in btn_list" :class="i.active_div" @click="child_page_change(j)" hover-class="navigator-hover">
				<span class="iconfont" v-html="i.icon"></span>
				<text type="default">{{i.text}}</text>
			</div>
		</div>
	</view>
</template>

<script>
	import Chat from "./wx_chat/wx_chat"
	import Contacts from "./wx_contacts/wx_contacts"
	import Find from "./wx_find/wx_find"
	import My from "./wx_my/wx_my"
	import "../../static/font/iconfont.css"
	export default {
		data() {
			return {
				title: 'Hello',
				child_page_num: 0,
				active_div: "active_div",
				userName:'',
				btn_list: [{
						text: "微信",
						icon: "&#xe715;",
						active_div: 'active_div',
					},
					{
						text: "通讯录",
						icon: "&#xe6c2;",
						active_div: ''
					},
					{
						text: "发现",
						icon: "&#xe60a;",
						active_div: ''
					},
					{
						text: "我",
						icon: "&#xe61e;",
						active_div: ''
					},
				]
			}
		},
		components: {
			Chat,
			Contacts,
			Find,
			My,
		},
		methods: {
			child_page_change(a) {
				this.child_page_num = a;
				this.btn_list.forEach((v, k) => {
					v.active_div = '';
				})
				this.btn_list[a].active_div = "active_div";
			}
		},
		mounted() {
			uni.getStorage({
				key: 'user_name',
				success: (res) => {
					this.userName = res.data
				},
				fail: () => {
					uni.navigateTo({
						url: '/pages/login/login',
						animationType: 'pop-in',
						animationDuration: 400,
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
			});
		}
	}
</script>

<style lang="scss">
	.content {
		text-align: center;
		height: 100vh;
		display: flex;
		flex-direction: column;
		overflow: hidden;
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
		.bottom_btn_box {
			height: 90upx;
			font-size: 26upx;
			display: flex;
			flex-direction: row;
			justify-content: space-around;
			background: #f1f5f9;

			div {
				height: 90upx;
				flex: 1;
				display: flex;
				flex-direction: column;
				justify-content: center;
				align-items: center;
				color: #666;

				.iconfont {
					font-size: 40upx;
				}

				text {
					text-align: center;
				}
			}

			.active_div {
				color: yellowgreen;
			}
		}
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
</style>
