<template>
	<view class="container">
		<textarea maxlength="-1" class="text-box" 
		:value="content"
		disabled="true"
		 @blur="bindTextAreaBlur" placeholder="扫描二维码后的内容"  />
		 
		 <view class="btn-box">
			<button  type="primary" @click="scan">扫描</button>
			<button v-show="content.length>0" type="primary" @click="copyContent">复制内容</button>
			<button v-show="content.length>0" type="primary" @click="clearContent">内容清空</button>
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
				// 允许从相机和相册扫码
				let _that = this;
				uni.scanCode({
					success: function (res) {
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
						_that.content=res.result;
					}
				});
			},
			copyContent(){
				let _that = this;
				uni.setClipboardData({
					data: _that.content,
					success:  () =>{
						uni.showToast({
							title: '复制成功',
							icon:"success",
							duration: 1000
						});
						
					}
				});

			},
			clearContent(){
				this.content='';
			},
			bindTextAreaBlur(e) {
				console.log(e.detail.value)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		padding: 20upx;
		.text-box{
			min-height: 200px;
			width: 100%;
			border:  1px solid antiquewhite;
		}
		
		.btn-box{
			margin-top: 20upx;
			
			button{
				margin-top: 10upx;
			}
		}
	}
	
</style>
