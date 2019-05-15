<template>
	<view class="wx_my">
		<p class="user_name">{{userName}}</p>
		<p class="out" @click="out()">退出登录</p>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:["userName"],
		methods:{
			out(){
				uni.clearStorage();
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
	}
</script>

<style scoped lang="scss">
.wx_my{
	flex:1;
	background:linear-gradient(top, #2468ac 10%, #efefef 100%);
	.user_name{
		width:250upx;
		height:250upx;
		margin:0 auto;
		background: linear-gradient(left top, #2468ac 10%, rgba(0, 0, 0, .8) 50%, #789ac9 100%);
		line-height: 250upx;
		border-radius:50%;
		color:#fff;
		margin-top:100upx;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}
	.out{
		text-align: center;
		width:250upx;
		border-radius:10upx;
		line-height: 60upx;
		border:1px solid #fff;
		color:#fff;
		margin:150upx auto 0; 
	}
}
</style>
