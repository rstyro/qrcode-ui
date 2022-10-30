<template>
	<view class="container">
		<textarea maxlength="10208" class="text-box" :value="content" @input="bindTextAreaBlur"
			placeholder="扫描二维码后的内容" />

		<view class="btn-box">
			<button type="primary" @click="scan">{{content.length>0?'继续扫描':'扫描'}}</button>
			<button v-show="content.length>0" type="primary" @click="copyContent">复制内容</button>
			<button v-show="content.length>0" type="primary" @click="toCode">生成二维码</button>
		</view>
		
		// #ifdef MP
			<view style="margin-top: 160px;">
				<ad unit-id="adunit-9fcb53b7b4c16fd4" ad-type="video" ad-theme="white"></ad>
			</view>
		// #endif
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
		onLoad() {
			// #ifdef MP
			// this.adLoad()
			// #endif
		},
		//分享
		onShareAppMessage(res) {
			if (res.from === 'menu') { // 来自页面内分享按钮
				console.log(res.target)
			}
			return {
				title: '皮卡二维码',
				path: '/pages/tabbar/scan/index'
			}
		},
		methods: {
			scan() {
				// 允许从相机和相册扫码
				let _that = this;
				uni.scanCode({
					success: function(res) {
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
						_that.content = res.result;
					}
				});
			},
			copyContent() {
				let _that = this;
				uni.setClipboardData({
					data: _that.content,
					success: () => {
						uni.showToast({
							title: '复制成功',
							icon: "success",
							duration: 1000
						});

					}
				});

			},
			bindTextAreaBlur(e) {
				this.content = e.detail.value;
			},
			toCode() {
				// 生成二维码
				//在起始页面跳转到test.vue页面并传递参数
				console.log("mark-:", this.content);
				if (this.content) {
					const text = encodeURIComponent(this.content);
					uni.navigateTo({
						url: '/pages/tabbar/tools/module/view-code?content=' + text
					});
				} else {
					uni.showToast({
						title: '请输入内容',
						icon: "error",
						duration: 1000
					});
				}
			},
			adLoad() {
				// 在页面中定义插屏广告
				let interstitialAd = null

				// 在页面onLoad回调事件中创建插屏广告实例
				if (wx.createInterstitialAd) {
					interstitialAd = wx.createInterstitialAd({
						adUnitId: 'adunit-8b4a96b8df41bf7b'
					});
					interstitialAd.onLoad(() => {
						console.log("广告加载成功")
					});
					interstitialAd.onError((err) => {
						console.log(err)
					});
					interstitialAd.onClose(() => {
						console.log("关闭广告")
					})
			}else{
				console.log("else-----");
			}

			// 在适合的场景显示插屏广告
			if (interstitialAd) {
				interstitialAd.show().catch((err) => {
					console.error(err)
				})
			}
		}
	}
	}
</script>

<style lang="scss" scoped>
	.container {
		padding: 20upx;

		$padding: 40rpx;

		.text-box {
			width: calc(100% - $padding);
			border: 1px solid antiquewhite;
			padding: 20rpx;
		}

		.btn-box {
			margin-top: 20upx;

			button {
				margin-top: 10upx;
			}
		}
	}
</style>
