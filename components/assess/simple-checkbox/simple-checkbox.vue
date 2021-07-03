<template>

	<!-- <view>
		<view v-for="itemGroup in itemGroupList">
			<view v-for="item in itemGroup">
				<view>
					<checkbox checked="true" :value="item.value" />
					{{item.text}}
				</view>
			</view>
		</view>
	</view> -->

	<view>
		<checkbox  v-bind:checked="checked"  v-bind:value="itemValue" />
		{{itemText}}
	</view>


</template>

<script>
	export default {
		name: 'simple-checkbox',
		props: {
			itemValue: {
				default: ''
			},
			itemText: {
				default: ''
			},
			checked:false ,
			itemList: []

		},
		data() {
			return {
				isOpen: false
			}
		},
		computed: {
			itemGroupList: function() {
				var resultData = this.itemList;
				var groupIndex = 3; //分成3个一组
				var result = [];
				for (var k = 0, len = resultData.length; k < len; k += groupIndex) {
					result.push(resultData.slice(k, k + groupIndex));
				}
				return result;
			}
		},

		methods: {

		}

	}
</script>

<style>
</style>
