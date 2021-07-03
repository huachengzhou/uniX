<template>
	<view class="vbutton">
		<button @click.stop="submitFun()" :loading="loading">
			<!-- 插槽默认值 -->
			<slot>
				<view>提交</view>
			</slot>
		</button>
	</view>
</template>

<script>
	export default {
		name: 'assess-submit-button',
		props: {
			loading: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {

			}
		},
		computed: {

		},

		methods: {
			submitFun: function() {
				this.$emit("submit");
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
		},
		beforeUpdate: function() {
			// console.group('beforeUpdate 更新前状态===============》');
		},
		updated: function() {
			// console.group('updated 更新完成状态===============》');
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
	.vbutton {
		padding: 0 11px 11px;
		color: #a5a5a5;
		line-height: 100rpx;
		flex: 0 0 100rpx;
	}
</style>
