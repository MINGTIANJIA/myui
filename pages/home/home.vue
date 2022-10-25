<template>
	<view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in list" :key="index">
				<image :src="item.image_src" mode=""></image>
			</swiper-item>
			
		</swiper>
		<view class="box">
			<view class="he" v-for="(item,index) in listtop" :key="index">
				<image :src="item.image_src" mode=""></image>
				
			</view>
			
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:[],
				listtop:[]
				
			};
		},
		mounted() {
			this.add()
			this.addimg()
		},
		methods:{
			async add(){
				let{data} =await uni.$http.get('/home/swiperdata')
				this.list=data.message
			},
			async addimg(){
				let{data} =await uni.$http.get('/home/catitems')
				this.listtop=data.message
			}
		}
	}
</script>

<style lang="scss">
	swiper-item{
		width: 100%;
		height: 250px;
		image{
			width: 100%;
			height: 100%;
		}
	}
.box{
	display: flex;
	.he{
		width: 25%;
		margin-top: 10px;
		display: flex;
		justify-content: center;
		align-items: center;
		image{
			width: 75px;
			height: 100px;
		}
	}
}
</style>
