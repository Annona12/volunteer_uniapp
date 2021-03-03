<template>
<view >
	这是志愿者服务平台的首页
	<view >
		{{msg}}
	</view>
	<view >
		<image :src="imageUrl" mode=""></image>
	</view>
	<view v-for="(item,index) in arr" :key="index">
		{{item.name}}:{{item.age}}
	</view>
	<button type="primary" @click="clickHandle(20,$event)">按钮</button>
	<button type="primary" @click="pullDown">下拉刷新</button>
	<view >
		<image :src="imageUrl" mode=""></image>
	</view>
	<view v-for="(item,index) in arr" :key="index">
		{{item.name}}:{{item.age}}
	</view>
	<button type="primary" @click="clickHandle(20,$event)">按钮</button>
	<button type="primary" @click="pullDown">下拉刷新</button>
	<button type="primary" @click="get">发送get请求</button>
	<button type="primary" @click="setStorage">存储数据</button>
	<button type="primary" @click="getStorage">获取数据</button>
	<button type="warn" @click="removeStorage">移除数据</button>
	<button type="primary" @click="uploadPhoto">上传图片</button>
<!-- <view class="">
<image v-for="item in imgarry" :src="item" mode="" @click="previewImg(item)"></image>
</view> -->
	<!-- #ifdef H5 -->
	<view class="">
		只在H5中显示
	</view>
	<!-- #endif  -->
	<!-- #ifdef MP-WEIXIN -->
	<view class="">
		只在微信小程序中显示
	</view>
	<!-- #endif -->
	<navigator url="/pages/login/login?id=80">跳转至登陆页面</navigator>
	<navigator url="/pagwarnes/login/login" open-type="redirect">跳转至首页面</navigator>
	<button type="default" @click="gotoDetail">跳转至详情页</button>
	<test v-if="flag" :title="title" @myevent="getNum"></test>
	<button type="primary" @click="changeTest">切换组件</button>
	<view>
	    <uni-calendar 
	    :insert="true"
	    :lunar="true" 
	    :start-date="'2019-3-2'"
	    :end-date="'2019-5-20'"
	    @change="change"
	     />
	</view>
</view>
</template>

<script>
	import test from '../../components/home//test.vue'
	import uniCalendar from '../../components/uni-calendar/uni-calendar.vue'
	export default{
		data(){
			return {
				title:'message',
				flag:true,
				msg:'hello,world',
				imgarry:[],
				imageUrl:'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fa0.att.hudong.com%2F30%2F29%2F01300000201438121627296084016.jpg&refer=http%3A%2F%2Fa0.att.hudong.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1617262761&t=9db72c035732deab87f684fd02a716b2',
				arr:[
					{
						name:'Li',age:10
					}
				]
			}
		},
		onLoad(){
			console.log('页面加载了')
			//#ifdef MP-WEIXIN
			console.log('在微信小程序中打印')
			//#endif
			//#ifdef H5
			console.log('在H5中打印')
			//#endif
		},
		methods:{
			clickHandle(num,e){
				console.log('点击了',num)
			},
			pullDown(){
				uni.startPullDownRefresh()
			},
			get(){
				uni.request({
					url:'http://localhost:3000/getposts',
					success(res){
						console.log(res)
					}
				})
			},
			setStorage(){
				// uni.setStorage({
				// 	key:'id',
				// 	data:80,
				// 	success(res){
				// 		console.log('存储成功')
				// 	}
				// })
				uni.setStorageSync('id',100)
		},
		getStorage(){
			uni.getStorage({
				key:'id',
				success(res){
					console.log('获取成功',res.data)
				}
			})
			},
			removeStorage(){
				uni.removeStorage({
					key:'id',
					success(){
						console.log('移除成功')
					}
				})
				},
		onPullDownRefresh(){
			console.log('更新了列表')
			//更新完成就将下拉更新暂停
			setTimeout(()=>{
				this.msg='更新了页面'
				uni.stopPullDownRefresh()
			},2000)
		},
		onReachBottom(){
			console.log('触发到底部了')
			this.arr.push(
			{
				name:'Li',age:11
			},{
						name:'Li',age:12
					}
			)
		},
		//选择图片上传
		uploadPhoto(){
			// console.log('上传图片')
			uni.chooseImage({
				count:5,
				success:res=>{
					// console.log(res)
					this.imgarry=res.tempFilePaths
				},
				
			})
		},
		//预览图片
		previewImg(current){
			// console.log(current)
			uni.previewImage({
				current:current,
				urls:this.imgarry,
				loop:true,
				indicator:'number'
			})
		},
		gotoDetail(){
			uni.navigateTo({
				url:'/pages/login/login'
			})
		},
		changeTest(){
			this.flag=!this.flag
		},
		getNum(num){
			console.log(num)
		},
		change(){
			console.log('触发了事件')
		}
	},
	components:{
		test,
		uniCalendar
	}
	}
</script>

<style> 
</style>
