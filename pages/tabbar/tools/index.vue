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
