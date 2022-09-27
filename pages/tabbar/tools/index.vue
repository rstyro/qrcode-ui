<template>
	<view class="container">
		<uni-card>
			<view class="item" @click="toMarkCode()">
				<view class="item-label">生成二维码</view>
				<view><uni-icons type="right" size="30"></uni-icons></view>
			</view>
		</uni-card>
	</view>
	
</template>

<script>
export default {
	data() {
		return {
			title: 'Hello'
		};
	},
	onLoad() {
		// this.test();
	},
	methods: {
		 toMarkCode(){
			 uni.navigateTo({
			 	url: '/pages/tabbar/tools/module/mark-code'
			 });
		},
		
	}
};
</script>

<style lang="scss" scoped>
.container {
	padding: 20upx;
	
	.item{
		display: flex;
		vertical-align: middle;
		
		.item-label{
			flex-grow: 1
		}
	}
}
</style>
