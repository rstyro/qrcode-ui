<template>
	<view class="container">
		<uni-card>
			<text>这是一个基础卡片示例，内容较少，此示例展示了一个没有任何属性不带阴影的卡片。</text>
			<uni-icons type="right" size="30"></uni-icons>
		</uni-card>
	</view>
	<!-- <vue-qr text="Hello world!"></vue-qr> -->
</template>

<script>
	// vue3.0 (support vite)
	import vueQr from 'vue-qr/src/packages/vue-qr.vue';
	import QrcodeDecoder from 'qrcode-decoder';
export default {
	data() {
		return {
			title: 'Hello'
		};
	},
	components:{vueQr },
	onLoad() {
		this.test();
	},
	methods: {
		 test(){
		},
	}
};
</script>

<style lang="scss">
.container {
	padding: 20upx;
}
</style>
