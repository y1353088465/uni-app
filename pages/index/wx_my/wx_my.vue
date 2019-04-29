<template>
	<view class="wx_my">
		{{userName}}
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:["userName"]
	}
</script>

<style scoped lang="scss">
.wx_my{
	flex:1;
}
</style>
