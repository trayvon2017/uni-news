<template>
	<view class="content">
		<view class="uni-list">
			<view @click="goNewsInfo(item.post_id)" class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in list" :key="index">
				<view class="uni-media-list">
					<image class="uni-media-list-logo" @error="handleImgError" :data-index="index" :src="item.author_avatar"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top">{{item.title}}</view>
						<view class="uni-media-list-text-bottom uni-ellipsis">{{item.created_at}}</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				list: []
			}
		},
		onLoad() {
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method: 'GET',
				data: {},
				success: res => {
					console.log(res);
					this.list = res.data
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			handleImgError (e) {
				console.log(e.target);
				let index = e.target.dataset.index
				this.list[index].author_avatar = '../../static/logo.png'
			},
			goNewsInfo (post_id) {
				uni.navigateTo({
					url: '../info/info?post_id=' + post_id,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style lang="scss">
	.content {
		text-align: center;
		height: 400upx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
	.uni-media-list-body{
		height: auto;
	}
</style>
