<template>
	<view class="">
		这是一个组件
		<button type="warn">自定义组件</button>
		{{title}}
		<button type="default" @click="sendNum">给父组件传值</button>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				num:8
			}
		},
		props:['title'],
		destroyed(){
			console.log('组件被摧毁')
		},
		methods:{
			sendNum(){
				console.log('给父组件传值')
				this.$emit('myevent',this.num)
			}
		}
	}
</script>

<style>
</style>
