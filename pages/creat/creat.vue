<template>
	<view>
		<view class="cate">
			<!-- 左侧导航 -->
			<scroll-view scroll-y="true" :style="{height:scrollHeight+'px',width:'120px'}"> 
				<view class="cate_nav" :class="{active:active==index}" @click="handler(index)" v-for="(item,index) in list" :key="index">
					{{item.cat_name}}
				</view>
			</scroll-view>
			<!-- 右侧 -->
			<scroll-view scroll-y="true" :style="{height:scrollHeight+'px',width:'100%'}">
				<view>
					<view class="leveltwo">
						/{{level2[0].cat_name}}/
						
					</view>
					<!-- 三级列表区域 -->
					<view class="levelthree">
						<view v-for="(item,index) in level2[0].children" :key="index">
							<image :src="item.cat_icon" mode="" @click="goList(item)"></image><br>
							<text>{{item.cat_name}}</text>
							
						</view>
						
					</view>
				</view>
			</scroll-view>
			
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:[],
				active:0,
				scrollHeight:0,
				level2:[]
				
			};
		},
		methods:{
			async add(){
				let{data} =await uni.$http.get('/categories')
				console.log(data);
				this.list=data.message
				this.level2=data.message[0].children
			},
			handler(index){
				this.active=index
				this.level2=this.list[index].children
				
			},
			goList(item){
				uni.navigateTo({
					url:'/subpkg/goods_list/goods_list?cid='+item.cat_id
				})
			}
			
		},
		
		mounted() {
			this.add()
			// 获取系统屏幕可使用高度
			uni.getSystemInfo({
				success:(res)=>{
					this.scrollHeight=res.windowHeight
					console.log(this.scrollHeight);
				}
			})
		}
		
	}
</script>

<style lang="scss">
	.cate{
		display: flex;
		background-color: #fff;
		.cate_nav{
			width: 100px;
			line-height: 60px;
			text-align: center;
			background-color: #fff;
			&.active{
				position: relative;
				&::before{
					content: '';
					display: block;
					background-color: #c00000;
					width: 3px;
					height: 30px;
					position: absolute;
					top: 50%;
					left: 3px;
					transform: translateY(-50%);
				}
			}
		}
		.leveltwo{
			line-height: 40px;
			text-align: center;
			background-color: #fff;
			
		}
		.levelthree{
			display: flex;
			flex-wrap: wrap;
			text-align: center;
			image{
				margin: 5px;
				width: 80px;
				height: 80px;
			}
		}
		
		
	}

</style>
