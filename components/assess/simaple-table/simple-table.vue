<template>
</template>

<script>
	export default {
		name: 'UniSimpleTable',
		props: {
			
		},
		methods: {
			onClick() {
				this.$emit('click')
			}
		}
	}
</script>

<style>
	@charset "UTF-8";
	/*
	 *  uni-app 表格样式表
	 *  作者:helang
	 *  邮箱:helang.love@qq.com
	*/
	.h-table {
	  /* 行 */
	  /* 单元格 */
	  /* 表头 */
	  /* 表格虚线 */
	  /* 表格主题 Map，颜色摘自 Bootstrap */
	  /* 生成主题代码 */
	}
	.h-table .h-tr {
	  box-sizing: border-box;
	  display: flex;
	  flex-direction: row;
	  flex-wrap: nowrap;
	  justify-content: flex-start;
	  align-items: stretch;
	  align-content: center;
	  border-color: #ccc;
	  border-style: solid;
	  border-width: 0;
	  border-top-width: 1px;
	  border-left-width: 1px;
	  border-bottom-width: 1px;
	  color: #333;
	  /* 等比分列，1-6列 */
	}
	.h-table .h-tr-1 > .h-td {
	  width: 100%;
	}
	.h-table .h-tr-2 > .h-td {
	  width: 50%;
	}
	.h-table .h-tr-3 > .h-td {
	  width: 33.3333333333%;
	}
	.h-table .h-tr-4 > .h-td {
	  width: 25%;
	}
	.h-table .h-tr-5 > .h-td {
	  width: 20%;
	}
	.h-table .h-tr-6 > .h-td {
	  width: 16.6666666667%;
	}
	.h-table .h-tr + .h-tr {
	  border-top-style: none;
	}
	.h-table .h-td {
	  box-sizing: border-box;
	  padding: 3px;
	  word-break: break-all;
	  border-color: #ccc;
	  border-style: solid;
	  border-width: 0;
	  border-right-width: 1px;
	  display: flex;
	  flex-direction: row;
	  flex-wrap: nowrap;
	  justify-content: center;
	  align-items: center;
	  align-content: center;
	  min-height: 64rpx;
	  /* 跨列 */
	  /* 内容顶部对齐 */
	  /* 内容底部对齐 */
	  /* 内容左边对齐 */
	  /* 内容右边对齐 */
	}
	.h-table .h-td-colspan {
	  flex-grow: 1;
	  width: 0;
	}
	.h-table .h-td-rowspan {
	  border-right-width: 0;
	  padding: 0 !important;
	  flex-wrap: wrap !important;
	}
	.h-table .h-td-rowspan > .h-tr {
	  width: 100%;
	  border-width: 0;
	}
	.h-table .h-td-rowspan > .h-tr .h-td {
	  border-right-width: 1px;
	}
	.h-table .h-td-rowspan > .h-tr + .h-tr {
	  border-top-width: 1px;
	  border-top-style: solid;
	}
	.h-table .h-td-top {
	  align-items: flex-start;
	  align-content: flex-start;
	}
	.h-table .h-td-bottom {
	  align-items: flex-end;
	  align-content: flex-end;
	}
	.h-table .h-td-left {
	  justify-content: flex-start;
	}
	.h-table .h-td-right {
	  justify-content: flex-end;
	}
	.h-table .h-thead {
	  background-color: #e6e6e6;
	}
	.h-table-dashed .h-tr {
	  border-top-style: dashed;
	  border-left-style: dashed;
	  border-bottom-style: dashed;
	}
	.h-table-dashed .h-td {
	  border-right-style: dashed;
	}
	.h-table-dashed .h-td-rowspan .h-tr + .h-tr {
	  border-top-style: dashed;
	}
	.h-table-primary .h-tr {
	  border-top-color: #2e6da4;
	  border-left-color: #2e6da4;
	  border-bottom-color: #2e6da4;
	  color: #337ab7;
	}
	.h-table-primary .h-td {
	  border-right-color: #2e6da4;
	}
	.h-table-primary .h-thead {
	  background-color: #337ab7;
	  color: #fff;
	}
	.h-table-success .h-tr {
	  border-top-color: #4cae4c;
	  border-left-color: #4cae4c;
	  border-bottom-color: #4cae4c;
	  color: #5cb85c;
	}
	.h-table-success .h-td {
	  border-right-color: #4cae4c;
	}
	.h-table-success .h-thead {
	  background-color: #5cb85c;
	  color: #fff;
	}
	.h-table-info .h-tr {
	  border-top-color: #46b8da;
	  border-left-color: #46b8da;
	  border-bottom-color: #46b8da;
	  color: #5bc0de;
	}
	.h-table-info .h-td {
	  border-right-color: #46b8da;
	}
	.h-table-info .h-thead {
	  background-color: #5bc0de;
	  color: #fff;
	}
	.h-table-warning .h-tr {
	  border-top-color: #eea236;
	  border-left-color: #eea236;
	  border-bottom-color: #eea236;
	  color: #f0ad4e;
	}
	.h-table-warning .h-td {
	  border-right-color: #eea236;
	}
	.h-table-warning .h-thead {
	  background-color: #f0ad4e;
	  color: #fff;
	}
	.h-table-danger .h-tr {
	  border-top-color: #d43f3a;
	  border-left-color: #d43f3a;
	  border-bottom-color: #d43f3a;
	  color: #d9534f;
	}
	.h-table-danger .h-td {
	  border-right-color: #d43f3a;
	}
	.h-table-danger .h-thead {
	  background-color: #d9534f;
	  color: #fff;
	}
</style>
