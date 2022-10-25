<template>
	<view>

	</view>
</template>

<script>
	import {
		mapState, 
		mapMutations
	} from 'vuex'
	export default {
		data() {
			return {
				shopList: []

				timer: null
			};
		},
		methods: {
			...mapMutations(['addHisList']),
			input(query) {
				this.timer && clearTimeout(this.timer)
				this.timer=setTimeout(()=>{
					this.getShopList(query)
				},500)

			},
			async getShopList(query){
				let{data} await uni.$http.get('/gooods/                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               ')
				
			}
			
		},
		computed:{
			...mapState(['hisList'])
		}
	}
</script>

<style lang="scss">

</style>
