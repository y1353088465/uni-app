<template>
	<view v-if="fog_status" class="fog">
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:["fog_status"]
	}
</script>

<style scoped lang="scss">
.fog{
	width:100%;
	height:100vh;
	background:rgba(0,0,0,.4);
	position: fixed;
	left:0;
	top:0;
	z-index: 1;
}
</style>
