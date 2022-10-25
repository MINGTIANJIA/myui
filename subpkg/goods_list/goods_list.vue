<template>
	<view>
		<view class="list_box" v-for="(item,index) in goodslist" :key="index">
			<view>
				<image :src="item.goods_big_logo || defaultimg" mode=""></image>
			</view>
			<view class="right_list">
				<view>
					{{item.goods_name}}
					
					
				</view>
				<text>${{item.goods_price}}</text>
				
			</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				defaultimg:'https://api-hmugo-web.itheima.net/pyg/banner1.png',
				goodslist:[],
				form:{
					query:'',
					cid:'',
					pagenum:1,
					pagesize:10
				},
				total:0
				
			};
		},
		mounted() {
			this.goGoodsList()
			
		},
		onLoad(obj){
			this.form.cid=obj.cid
		},
		onPullDownRefresh() {
			this.form.pagenum=1,
			this.goodslist=[]
			this.goGoodsList()
		},
		
		methods:{
		  async	goGoodsList(){
			  let{data} =await uni.$http.get('/goods/search',this.form)
			  console.log(data);
			  this.goodslist=[...this.goodslist,...data.message.goods]
			  this.total=data.message.total
				
			}
		}
		
	}
</script>

<style lang="scss">
	view{
		background-color: white;
	}
	.list_box{
		
		display: flex;
		margin-top: 10px;
		border-bottom: 1px solid gray;
		image{
		width: 100px;
		height: 100px;
		}
		text{
			color: red;
		}
		.right_list{
			margin-left: 10px;
		}
		
	}

</style>
