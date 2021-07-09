<template>
	<view>
		<view>
			<view>
				<page-head :title="title"></page-head>
				<view class="uni-padding-wrap">
					<view style="background:#FFFFFF; padding:40rpx;">
						<view class="uni-hello-text uni-center">当前位置信息</view>
						<block v-if="hasLocation === false">
							<view class="uni-h2 uni-center uni-common-mt">未选择位置</view>
						</block>
						<block v-if="hasLocation === true">
							<view class="uni-hello-text uni-center" style="margin-top:10px;">
								{{locationAddress}}
							</view>
							<view class="uni-h2 uni-center uni-common-mt">
								<text>E: {{location.longitude[0]}}°{{location.longitude[1]}}′</text>
								<text>\nN: {{location.latitude[0]}}°{{location.latitude[1]}}′</text>
							</view>
						</block>
					</view>
					<view class="uni-btn-v">
						<button type="primary" @tap="chooseLocation">选择位置</button>
						<button @tap="clear">清空</button>
					</view>
				</view>
			</view>
		</view>
		<view>
			<page-head :title="title"></page-head>
			<view class="uni-common-mt">
				<view>
					<map :latitude="latitude" :longitude="longitude" :markers="covers">
					</map>
				</view>
			</view>
		</view>
		
		<view>
			<page-head :title="'地图搜索'"></page-head>
			<view class="uni-common-mt">
				<view>
					<map id="mapSource" ref="mapSource"></map>
				</view>
			</view>
		</view>

	</view>


</template>
<script>
	import util from '../../common/util.js';
	import page_foot from '@/components/page-foot/page-foot.vue';
	import page_head from '@/components/page-head/page-head.vue';

	var formatLocation = util.formatLocation;


	module.exports = {
		data() {
			return {
				title: 'chooseLocation',
				hasLocation: false,
				location: {},
				locationAddress: '',
				latitude: 39.909,
				longitude: 116.39742,
				covers: [{
					latitude: 39.9085,
					longitude: 116.39747,
					// #ifdef APP-PLUS
					iconPath: '../../../static/app-plus/location@3x.png',
					// #endif
					// #ifndef APP-PLUS
					iconPath: '../../../static/location.png',
					// #endif
				}, {
					latitude: 39.90,
					longitude: 116.39,
					// #ifdef APP-PLUS
					iconPath: '../../../static/app-plus/location@3x.png',
					// #endif
					// #ifndef APP-PLUS
					iconPath: '../../../static/location.png',
					// #endif
				}]
			}
		},
		components: {
			"page-head": page_head,
			"page-foot": page_foot,
		},
		methods: {
			chooseLocation: function() {
				uni.chooseLocation({
					success: (res) => {
						console.log(res);
						this.hasLocation = true,
							this.location = formatLocation(res.longitude, res.latitude),
							this.locationAddress = res.address
					}
				})
			},
			clear: function() {
				this.hasLocation = false
			},

		}
	}
</script>

<style>
	.page-body-info {
		padding-bottom: 0;
		height: 440rpx;
	}

	.content {
		flex: 1;
	}

	.map {
		width: 750rpx;
		height: 500rpx;
		background-color: black;
	}

	.scrollview {
		flex: 1;
	}

	.button {
		margin-top: 30rpx;
		margin-bottom: 20rpx;
	}
</style>
