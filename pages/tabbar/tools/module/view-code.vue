<template>
	<view class="container">
		<canvas type="2d" style="width: 260px; height: 260px;margin: 20rpx auto;" id="myQrcode"></canvas>
		<view class="btn-box">
			<button type="primary" @click="downloadImg">下载二维码</button>
			<button type="primary" @click="toBack">返回编辑</button>
		</view>
	</view>
</template>

<script>
	import drawQrcode from 'weapp-qrcode-canvas-2d';
	
	export default {
		data() {
			return {
				content: '',
				filePath:''
			}
		},
		onLoad(option) {
			if(option.content){
				this.content=decodeURIComponent(option.content);
			}
		},
		onShow() {
			if(this.content){
				this.handleMakeQrcode(this.content);
			}
		},
		created() {
		},
		methods: {
			downloadImg() {
				uni.saveImageToPhotosAlbum({
					filePath: this.filePath,
					success: () =>{
						console.log('this.filePath：',this.filePath);
						uni.showToast({
							title: '保存成功',
							icon: "success",
							duration: 500
						});
					}
				});
			},

			toBack() {
				uni.navigateBack({
					delta: 1
				});
			},
			/**
			* 生成二维码（没有使用叠加图片）
			* text - 码值
			* */
			handleMakeQrcode(text) {
				console.log("text:",text);
				let _that = this;
			    return new Promise((resolve, reject) => {
			    	const query = uni.createSelectorQuery()
			    	query.select('#myQrcode').fields({
			    		node: true,
			    		size: true
			    	}).exec((res) => {
			    		// 获取node节点实例，目前仅微信，快手，京东小程序支持；
			    		// #ifdef MP-WEIXIN || MP-KUAISHOU
			    		let canvas = res[0].node
			    		// #endif
			    		// 调用方法drawQrcode生成二维码
			    		drawQrcode({
			    			// #ifdef MP-WEIXIN || MP-KUAISHOU
			    			canvas: canvas,
			    			// #endif
			    			canvasId: 'myQrcode',
			    			width: 260,
			    			padding: 20,
							paddingColor:'#ffe',
			    			background: '#ffffff',
			    			foreground: '#000000',
			    			text: text,
			    		})
			    		// 获取临时路径
			    		uni.canvasToTempFilePath({
			    			canvasId: 'myQrcode',
			                // #ifdef MP-WEIXIN || MP-KUAISHOU
			    			canvas: canvas,
			                // #endif
			    			x: 0,
			    			y: 0,
			    			success(res) {
								console.log("res.tempFilePath:",res.tempFilePath);
								_that.filePath=res.tempFilePath;
			                    resolve(res.tempFilePath); // 临时路径
			    			},
			    			fail(res) {
			    			    console.error(res);
			                    reject();
			    			}
			    		})
			    	});
			    })
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		padding: 20upx;
		text-align: center;

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
