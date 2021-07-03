<template>
	<view class="uni-default-box">
		<picker @change="bindRangeChange($event)" :value="indexAssess" :range="itemList" :range-key="dataName">
			<view class="uni-input">
				{{selectName}}
			</view>
		</picker>
	</view>
</template>

<script>
	import * as utils from "../../../common/untils.js";


	export default {
		name: 'assess-picker',
		props: {
			dataList: {
				type: Array,
				default: []
			},
			dataName: {
				type: [String, Number],
				default: "name"
			},
			dataId: {
				type: [String, Number],
				default: "id"
			},
			dataInput: {
				type: [String, Number],
				default: ""
			},
			dataValue: {
				type: [String, Number],
				default: ""
			}
		},
		data() {
			return {
				indexAssess: 0,
				selectName: ""
			}
		},
		computed: {
			itemList: function() {
				let _this = this;
				var resultData = this.dataList;
				var result = [];
				resultData.forEach(function(item) {
					if (_this.dataName) {
						item.text = item[_this.dataName];
					}
					if (_this.dataId) {
						item.value = item[_this.dataId];
					}
					result.push(item);
				});
				return result;
			}
		},

		methods: {
			bindRangeChange: function(e) {
				let _this = this;
				let listData = this.itemList;
				let id = this.dataId;
				_this.indexAssess = e.detail.value;
				let dataName = _this.dataName;
				let pack = {
					dataList: _this.dataList,
					dataName: _this.dataName,
					dataId: _this.dataId,
					dataInput: _this.dataInput
				};
				let item = listData[_this.indexAssess];
				let obj = {
					item: item,
					pack: pack
				};
				// console.log("obj", obj);
				this.selectName = item[dataName];
				this.$emit("dataResult", obj);
			},
			initFun: function() {
				let dataList = this.dataList;
				let dataValue = this.dataValue;
				let _this = this;
				if (utils.isArrayNotEmpty(dataList)) {
					if (utils.isNotEmptyString(dataValue)) {
						for (var i = 0; i < dataList.length; i++) {
							let item = dataList[i];
							let resultValue = item[_this.dataId];
							if (utils.isNumber(dataValue)) {
								// console.log("equals:" + Number(resultValue) + " " + Number(dataValue));
								if (Number(resultValue) == Number(dataValue)) {
									_this.indexAssess = i;
									_this.selectName = item[_this.dataName];
								}
							}
							if (!utils.isNumber(dataValue)) {
								// console.log("equals:" + resultValue + " " + dataValue);
								if (resultValue == dataValue) {
									_this.indexAssess = i;
									_this.selectName = item[_this.dataName];
								}
							}
							// console.log("resultValue:" + resultValue);
						}
					}
				}
				// console.log("test2");
				// console.log(dataList);
				// console.log("dataValue:" + dataValue);
				// console.log("selectName:" + _this.selectName);
				// console.log("indexAssess:" + _this.indexAssess);
			}
		},
		beforeCreate: function() {
			// console.group('beforeCreate 创建前状态===============》');
		},
		created: function() {
			// console.group('created 创建完毕状态===============》');
			// console.log(this.$props);
			// console.log(this.$attrs);
			// console.log(this.$listeners);
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
			this.initFun();
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
