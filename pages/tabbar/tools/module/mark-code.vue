<template>
	<view class="container">
		<textarea maxlength="-1" class="text-box" :value="content" 
		@blur="bindTextAreaBlur"  @focus="bindTextAreaBlur" @confirm="bindTextAreaBlur"
		placeholder="二维码后的内容" />
		<view class="btn-box">
			<button type="primary" @click="toCode">生成二维码</button>
			<button v-show="content.length>0" type="primary" @click="clearContent">内容清空</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				content: ''
			}
		},
		onLoad() {},
		methods: {
			toCode() {
				// 生成二维码
				//在起始页面跳转到test.vue页面并传递参数
				console.log("mark-:", this.content);
				uni.navigateTo({
					url: '/pages/tabbar/tools/module/view-code?content=' + this.content
				});

			},
			bindTextAreaBlur(e) {
				this.content=e.detail.value;
			},
			clearContent() {
				this.content = '';
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		padding: 20upx;

		.text-box {
			min-height: 200px;
			width: 100%;
			border: 1px solid antiquewhite;
		}

		.btn-box {
			margin-top: 20upx;

			button {
				margin-top: 10upx;
			}
		}
	}
</style>
