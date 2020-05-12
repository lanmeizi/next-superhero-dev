<template name="helloComp">
	<view>
		{{msg}}
		<view>
			<input type="text" :value="myvue" class="txt" />
		</view>
	</view>
</template>

<script>
	export default {
		name: 'helloComp',
		props: {
			myvue: {
				type: String,
				default: ''
			}
		},
		data() {
			return {
				msg: '自定义组件'
			}
		}
	}
</script>

<style>
	.txt {
		color: red;
	}
</style>
