<template>
	<view>
		<view class="uni-default-box">
			<view v-if="imageList.length > 0">
				<view v-for="(item, index) in imageList">
					<uni-link href="item.downloadUrl" text="下载" showUnderLine="false" color="#0000FF"></uni-link>
					<view>
						{{item.fileName}}
					</view>
					<button @click="deleteAttachmentById(item.attachmentId)" class="mini-btn" type="primary" size="mini">X</button>
				</view>
			</view>
		</view>

		<view class="uni-default-box">
			<button class="mini-btn" @click="chooseImage()" type="primary" size="mini">选择图片</button>
		</view>

	</view>
</template>

<script>
	import * as utils from "../../common/untils.js";

	export default {
		name: 'common-image-picker',
		props: {
			dataObj: {
				type: Object,
				default: {}
			},
			count: {
				type: [String, Number],
				default: 5
			}
		},
		data() {
			return {
				imageList: [],
				selectName: ""
			}
		},
		computed: {

		},
		methods: {
			deleteAttachmentById(id) {
				var _this = this;
				let query = {
					attachmentIds: id
				};
				let url = "/app.public/deleteAttachmentByIds";
				let option = {
					query: query,
					notParam: true,
					url: url + "?" + utils.parseParam(query),
					successCallback: function() {
						_this.initFun();
					}
				};
				utils.requestDefault(option);
			},
			setPaths: function(filePaths) {
				let query = this.dataObj;
				var _this = this;
				var userInfo = _this.$helper.fetchLocalUser();
				// 文件路径封装
				let objs = filePaths.map((value, index) => {
					return {
						name: "image" + index,
						uri: value
					}
				});
				uni.uploadFile({
					url: `${this.$config.server.host}/app.public/uploadFiles`,
					files: objs,
					formData: query,
					header: {
						"sign-value": _this.$helper.requestSign({}),
						"company-key": userInfo.userAccount
					},
					success: (res) => {
						if (res.statusCode === 200) {
							_this.initFun();
							uni.showToast({
								title: "成功!"
							});
						}
					}
				});
			},
			chooseImage: function() {
				var _this = this;
				uni.chooseImage({
					count: _this.count,
					sizeType: ['compressed'],
					sourceType: ['album'],
					success: (res) => {
						_this.setPaths(res.tempFilePaths);
					},
					fail: (err) => {
						console.log('chooseImage fail', err)
						// #ifdef MP
						uni.getSetting({
							success: (res) => {
								let authStatus = res.authSetting['scope.album'];
								if (!authStatus) {
									uni.showModal({
										title: '授权失败',
										content: 'Hello uni-app需要从您的相册获取图片，请在设置界面打开相关权限',
										success: (res) => {
											if (res.confirm) {
												uni.openSetting()
											}
										}
									})
								}
							}
						});
						// #endif
					}
				});
			},
			bindChange: function(e) {
				let _this = this;

				// this.$emit("dataResult", obj);
			},
			initFun: function() {
				let query = this.dataObj;
				var _this = this;
				if (!query.tableId) {
					return false;
				}
				let option = {
					url: "/app.public/downloadFtpFileToLocalByAttachmentDto",
					query: query,
					successCallback: function(resultData) {
						_this.imageList = resultData;
					}
				};
				utils.requestDefault(option);
			}
		},
		beforeCreate: function() {
			// console.group('beforeCreate 创建前状态===============》');
		},
		created: function() {
			// console.group('created 创建完毕状态===============》');
		},
		beforeMount: function() {
			// console.group('beforeMount 挂载前状态===============》');
			// console.log("%c%s", "color:red", "data   : ", this.$data); //已被初始化  
		},
		mounted: function() {
			// console.group('mounted 挂载结束状态===============》');
			this.initFun();
		},
		beforeUpdate: function() {
			// console.group('beforeUpdate 更新前状态===============》');
			// this.initFun();
		},
		updated: function() {
			// console.group('updated 更新完成状态===============》');
			// this.initFun();
		},
		beforeDestroy: function() {
			// console.group('beforeDestroy 销毁前状态===============》');
		},
		destroyed: function() {
			// console.group('destroyed 销毁完成状态===============》');
		}
	}
</script>

<style>
	.uni-default-box {
		border: 1px solid #E5E5E5;
		border-radius: 1px;
		padding: 0px 0px;
		/* #ifndef APP-NVUE */
		box-sizing: border-box;
		cursor: pointer;
		/* #endif */
	}
</style>
