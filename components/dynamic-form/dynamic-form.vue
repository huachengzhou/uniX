<template>
	<view>
		<uni-forms :modelValue="formData" ref="form" validate-trigger="bind" err-show-type="undertext" :rules="rules">
			<template v-for="(item,index) in formItems">
				<uni-forms-item v-if="'inputText'=== item.type" :required="item.required" :name="item.field" :label="item.fieldName" label-align="right" >
					<uni-easyinput type="text" v-model="formData[item.field]" :placeholder="item.fieldName" ></uni-easyinput>
				</uni-forms-item>
				<uni-forms-item v-if="'inputNumber'=== item.type" :required="item.required" :name="item.field" :label="item.fieldName" label-align="right" >
					<uni-easyinput :maxlength="item.maxlength && item.maxlength > 0 ? item.maxlength : 3 " 
						type="number" v-model="formData[item.field]" :placeholder="item.fieldName" ></uni-easyinput>
				</uni-forms-item>
				<uni-forms-item v-if="'textarea'=== item.type" :required="item.required" :name="item.field" :label="item.fieldName" label-align="right" >
					<uni-easyinput  
						type="textarea" v-model="formData[item.field]" :placeholder="item.fieldName" ></uni-easyinput>
				</uni-forms-item>
				<uni-forms-item v-if="'picker'=== item.type" :required="item.required" :name="item.field" :label="item.fieldName" label-align="right" >
					<picker @change="pickerChange(item,$event)" :value="item.pickerIndex" :range="item.pickerList" range-key="name">
						<view class="uni-input">{{item.pickerList[item.pickerIndex].name}}</view>
					</picker>	
				</uni-forms-item>
				<uni-forms-item v-if="'datetime'=== item.type" :required="item.required" :name="item.field" :label="item.fieldName" label-align="right" >
					<uni-datetime-picker   type="datetime"  v-model="formData[item.field]"   @change="dateTimeChange(item,$event)"></uni-datetime-picker>	
				</uni-forms-item>
				<uni-forms-item v-if="'date'=== item.type" :required="item.required" :name="item.field" :label="item.fieldName" label-align="right" >
					<uni-datetime-picker   type="date"  v-model="formData[item.field]"   @change="dateTimeChange(item,$event)"></uni-datetime-picker>	
				</uni-forms-item>
			</template>
		</uni-forms>
	</view>
</template>

<script>
	export default {
		name:"dynamic-form",
		props:{
			formItems:{type:Array,default:[]}
		},
		data() {
			return {
				formData:{
					
				},
				rules:{
					
				}
			};
		},
		watch:{
			formItems(data){
				if (!(Array.isArray(data))) {
					console.log("the props datas type must be array")
					return
				}
				this.builderFormDataField();
				this.builderRules();
			}
		},
		created() {
			this.builderFormDataField();
			this.builderRules();
			console.log(JSON.stringify(this.rules))
			
		},
		methods:{
			//初始化表单字段
			builderFormDataField(){
				this.formItems.forEach((item,index)=>{
					this.$set(this.formData,item.field,'');
					if('picker' === item.type){
						// console.log(JSON.stringify(item.pickerList[item.pickerIndex]))
						this.$set(this.formData,item.field,item.pickerList[item.pickerIndex].name);
					}
				})
				
				
			},
			//初始化表单校验规则
			builderRules(){
				this.formItems.forEach((item,index)=>{
					if(item.required){
						this.$set(this.rules,item.field,{rules:[ { required:true,
									errorMessage:item.fieldName+"为必填字段",
								}
						]});
					}
					
				})
			},
			//检验表单并返回表单值
			getFormData(){
				//动态表单校验状态
				let checkDynamicFrom = false;
				 this.$refs.form.validate().then((res)=>{
					console.log("res动态表单:"+ JSON.stringify(res))
					this.$emit("getResults",res);
					checkDynamicFrom = true;
					//异步会后执行，在设置一次值
					this.$emit("validateDynamicFrom",checkDynamicFrom);
				});
				//校验通过的情况下，会先于值修改前执行
				this.$emit("validateDynamicFrom",checkDynamicFrom);
			},
			//选择器选择变化事件
			pickerChange(item,e){
				console.log(e.detail.value)
				item.pickerIndex = e.detail.value;
				this.formData[item.field] = item.pickerList[item.pickerIndex].name;
			},
			//时间选择器变化事件
			dateTimeChange(item,e){
				console.log("dateTimeChange:"+ e);
				this.formData[item.field] = e;
			}
		}
	}
</script>

<style>

</style>
