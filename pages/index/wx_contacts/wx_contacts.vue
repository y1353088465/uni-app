<template>
	<view class="wx_contacts">
		<IndexHeader v-on:menu_status="menu_status" msg="通讯录"></IndexHeader>
		<div class="content">
			<view class="page-section page-section-gap" style="text-align: center;">
				<audio autoplay style="text-align: left" :src="current.src" :poster="current.poster" :name="current.name" :author="current.author"
				 :action="audioAction" controls></audio>
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
				menu_list_status: false,
				current: {
					poster: 'http://star.kuwo.cn/star/starheads/180/50/91/3314442120.jpg',
					name: '致爱丽丝',
					author: '暂无',
					src: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/audio/music.mp3',
				},
				audioAction: {
					method: 'pause'
				}
			};
		},
		mounted() {
			uni.vibrateLong({
				success: function() {
					console.log('success');
				}
			});
			uni.getProvider({
				service: 'push',
				success: function(res) {
					console.log(res.provider)
					// 个推的名称为 igexin
					if (~res.provider.indexOf('igexin')) {
						uni.subscribePush({
							provider: 'igexin',
							success: function(res) {
								console.log('success:' + JSON.stringify(res));
							}
						});
					}
				}
			});

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
			sao() {
				// 允许从相机和相册扫码
				uni.scanCode({
					success: function(res) {
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
					}
				});
			}
		}
	}
</script>

<style scoped lang="scss">
	.wx_contacts {
		flex: 1;
		display: flex;
		flex-direction: column;
		position: relative;

		.content {
			flex: 1;
		}
	}
</style>
