<template>
	<view>
		<view class="uni-default-box">
			<view v-if="fileList.length > 0">
				<view v-for="(item, index) in fileList">
					<uni-link href="item.downloadUrl" text="下载" showUnderLine="false" color="#0000FF"></uni-link>
					<view>
						{{item.fileName}}
					</view>
					<button @click="deleteAttachmentById(item.attachmentId)" class="mini-btn" type="primary"
						size="mini">X</button>
				</view>
			</view>
		</view>

		<view class="uni-default-box">
			<uni-file-picker @delete="deleteFun" mode="grid" v-model="imageValue" @select="select" @progress="progress"
				@success="success" @fail="fail" :limit="count" :file-mediatype="mediatype" :title="title">
				<button class="mini-btn" type="primary" size="mini">选择附件</button>
			</uni-file-picker>
		</view>

	</view>
</template>

<script>
	/*
	
	选择文件类型,all 只支持 H5 和微信小程序平台
	但是一共只有三个类型,image/video/all  ,因此本组就默认是all
	android 和 ios不支持
	*/
	import * as utils from "../../common/untils.js";

	export default {
		name: 'common-file-picker',
		props: {
			dataObj: {
				type: Object,
				default: {}
			},
			count: {
				type: [String, Number],
				default: 5
			},
			mediatype: {
				type: [String],
				default: "all"
			}
		},
		data() {
			return {
				fileList: [],
				selectName: "",
				imageValue: []

			}
		},
		computed: {
			title: function() {
				return "最多选择" + this.count + "个文件";
			}
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
			deleteFun(e) {
				console.log(e) ;
			},
			// 获取上传状态
			select(e) {
				var _this = this;
				console.log('选择文件：', e);
				console.log(_this.imageValue);
				var userInfo = _this.$helper.fetchLocalUser();
				let query = this.dataObj;
				// 文件路劲封装
				let objs = e.tempFiles;
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
							uni.showToast({
								title: "成功!"
							});
							_this.initFun();
						}
					}
				});
			},
			// 获取上传进度
			progress(e) {
				console.log('上传进度：', e)
			},
			// 上传成功
			success(e) {
				console.log('上传成功')
			},
			// 上传失败
			fail(e) {
				console.log('上传失败：', e)
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
						_this.fileList = resultData;
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
