<template>
	<view class="container">
		<uni-card>
			<view class="item" @click="toMarkCode()">
				<view class="item-label">生成二维码</view>
				<view class="item-icon">
					<uni-icons type="right" size="20"></uni-icons>
				</view>
			</view>
		</uni-card>

		<uni-card>
			<view class="item" @click="toScanCode()">
				<view class="item-label">扫描二维码</view>
				<view class="item-icon">
					<uni-icons type="right" size="20"></uni-icons>
				</view>
			</view>
		</uni-card>

		<uni-card>
			<view class="item" @click="toAvatar()">
				<view class="item-label">国庆头像合成</view>
				<view class="item-icon">
					<uni-icons type="right" size="20"></uni-icons>
				</view>
			</view>
		</uni-card>
		
		// #ifdef MP
		<uni-card>
			<view class="item">
				<ad unit-id="adunit-b498c5122298dcb9"></ad>
			</view>
		</uni-card>
		// #endif
		

	</view>

</template>

<script>
	export default {
		data() {
			return {
				canClick: true
			};
		},
		onLoad() {
			// this.test();
		},
		//分享
		onShareAppMessage(res) {
			if (res.from === 'menu') {// 来自页面内分享按钮
			  console.log(res.target)
			}
			return {
			  title: '皮卡二维码',
			  path: '/pages/tabbar/scan/index'
			}
		  },
		methods: {
			toMarkCode() {
				this.toPage("/pages/tabbar/tools/module/mark-code");
			},

			toPage(url) {
				let _that = this;
				if (this.canClick) {
					uni.navigateTo({
						url: url
					});
					setTimeout(() => {
						_that.canClick = true;
					}, 2000)
				} else {
					uni.showToast({
						title: '正在跳转...',
						icon: "success",
						duration: 1000
					});
				}
			},

			toScanCode() {
				uni.switchTab({
					url: '/pages/tabbar/scan/index'
				});

			},
			toAvatar() {
				this.toPage("/pages/tabbar/tools/module/avatar-mix");
			}

		}
	};
</script>

<style lang="scss" scoped>
	.container {
		padding: 20upx;

		.item {
			display: flex;
			vertical-align: middle;
			height: 70rpx;
			line-height: 70rpx;

			.item-label {
				flex-grow: 1;
			}

			.item-icon {}
		}
	}
</style>
