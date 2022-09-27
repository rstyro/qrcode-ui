<template>
	<view class="container">
		<textarea maxlength="-1" class="text-box" 
		:value="content"
		disabled="true"
		 @blur="bindTextAreaBlur" placeholder="扫描二维码后的内容"  />
		 
		 <view class="btn-box">
			<button  type="primary" @click="scan">扫描</button>
			<button type="primary">复制内容</button>
		 </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				content:''
			}
		},
		onLoad() {

		},
		methods: {
			scan(){
				this.content="aaaaaaaaaaaaaaaaaaa"
			},
			bindTextAreaBlur(e) {
				console.log(e.detail.value)
			}
		}
	}
</script>

<style lang="scss">
	.container {
		padding: 20upx;
		.text-box{
			min-height: 200px;
			width: 100%;
			border:  1px solid antiquewhite;
		}
		
		.btn-box{
			
			button{
				margin-top: 10upx;
			}
		}
	}
	
</style>
