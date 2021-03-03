<template>
	<view >
		这是login页面
		<navigator url="/pages/home/home" open-type="switchTab">跳转至首页面</navigator>
		<button type="primary" @click="gotoHome">回到首页</button>
	</view>
</template>

<script>
	
	export default{
		data(){
			return{
				
			}
		},
		
		onLoad(options){
			console.log(options)
		},
		methods:{
			gotoHome(){
				uni.switchTab({
					url:'/pages/home/home'
				})
			}
		},
		
	}
</script>

<style>
</style>
