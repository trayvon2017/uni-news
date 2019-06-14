<template>
	<view class="content">
		<view class="title">
			{{title}}
		</view>
		<view class="art-content">
			<rich-text class="richText" :nodes="content"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '',
				content: ''
			}
		},
		onLoad: function (e) {
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/' + e.post_id,
				method: 'GET',
				data: {},
				success: res => {
					console.log(res)
					let newsInfo = res.data
					this.title = newsInfo.title
					this.content = newsInfo.content
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style lang="scss">
	.content{
		padding: 10upx 2%;
		flex-wrap: wrap;
		.title{
			line-height: 2em;
			font-weight: 700;
			font-size: 38upx;
		}
		.art-content{
			line-height: 2em;
		}
	}
</style>
