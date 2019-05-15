<template>
	<view class="wx_find">
		<IndexHeader v-on:menu_status="menu_status" msg="发现"></IndexHeader>
		<MenuList v-on:menu_hide="menu_hide" v-on:pages_index="pages_index" v-if="menu_list_status"></MenuList>
	</view>
</template>

<script>
	import IndexHeader from "../../../components/index_header.vue"
	import MenuList from "../../../components/menu_list.vue"

	export default {
		data() {
			return {
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
			//监听子元素事件传输值
			menu_hide(value) {
				this.menu_list_status = value;
			},
		}
	}
</script>

<style scoped lang="scss">
	.wx_find {
		flex: 1;
	}
</style>
