<template>
	<view class="page">
		<!-- <helloComp myvue="hello Next"></helloComp>
		<trailerStars innerScore="5.1" showNum="1"></trailerStars> -->
		<!-- 轮播图开始 -->
		<swiper class="carousel" :indicator-dots="true" :autoplay="true">
			<swiper-item>
				<image src="../../static/logo.png" class="carousel"></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/tabBarIco/index_sel.png" class="carousel"></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/tabBarIco/me_sel.png" class="carousel"></image>
			</swiper-item>
		</swiper>
		<!-- 轮播图结束 -->
		<!-- 热门超英开始 -->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/logo.png" class="hot-ico" mode=""></image>
				<view class="hot-title">
					热门超英
				</view>
			</view>
		</view>
		<scroll-view scroll-x="true" class="page-block hot">
			<view class="single-poster" v-for="(moive, index) in moives" :key="index">
				<view class="poster-wapper">
					<image src="../../static/logo.png" class="poster" mode=""></image>
					<view class="movie-name">
						蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠蝙蝠侠{{moive}}
					</view>
					<!-- <view class="movie-score-wapper">
						<image src="../../static/tabBarIco/index_sel.png" class="star-ico"></image>
						<image src="../../static/tabBarIco/index_sel.png" class="star-ico"></image>
						<image src="../../static/tabBarIco/index_sel.png" class="star-ico"></image>
						<image src="../../static/tabBarIco/index_sel.png" class="star-ico"></image>
						<image src="../../static/tabBarIco/index.png" class="star-ico"></image>
						<view class="movie-score">9.1</view>
					</view> -->
					<trailerStars innerScore="7.1" showNum="1"></trailerStars>
				</view>
			</view>
		</scroll-view>
		<!-- 热门超英结束 -->
		<!-- 热门预告开始 -->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/logo.png" class="hot-ico" mode=""></image>
				<view class="hot-title">
					热门预告
				</view>
			</view>
		</view>
		<view class="hot-movies page-block">
			<video 
				v-for="trailer in hotTraileroList"
				:src="trailer.trailer" 
				:poster="trailer.poster"
				class="hot-movie-single"
				controls></video>
		</view>
		<!-- 热门预告结束 -->
		<!-- 猜你喜欢开始 -->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/logo.png" class="hot-ico" mode=""></image>
				<view class="hot-title">
					猜你喜欢
				</view>
			</view>
		</view>
		<view class="page-block guess-u-like">
			<view class="single-like-movie" v-for="(guess, gindex) in guessULikeList">
			<!-- <view class="single-like-movie"> -->
				<image src="../../static/logo.png" class="like-moive" mode=""></image>
				<view class="movie-desc">
					<view class="movie-title">
						蝙蝠侠大战超人好久看卡好看看卡
					</view>
					<trailerStars innerScore="9.1" showNum="0"></trailerStars>
					<view class="movie-info">
						2018/美国/动作/科幻
					</view>
					<view class="movie-info">
						麦当娜/麦当娜111/麦当娜222/麦当娜333/麦当娜444/麦当娜555
					</view>
				</view>
				<view class="movie-oper" :data-gindex="gindex" @click="praiseMe">
					<image src="../../static/tabBarIco/me_sel.png" class="praise-ico" mode=""></image>
					<view class="praise-me">点赞</view>
					<view :animation="animationDataArr[gindex]" class="praise-me animation-opacity">+1</view>
				</view>
			</view>
			<!-- <view class="single-like-movie">
				<image src="../../static/logo.png" class="like-moive" mode=""></image>
				<view class="movie-desc">
					<view class="movie-title">
						蝙蝠侠大战超人好久看卡好看看卡
					</view>
					<trailerStars innerScore="9.1" showNum="0"></trailerStars>
					<view class="movie-info">
						2018/美国/动作/科幻
					</view>
					<view class="movie-info">
						麦当娜/麦当娜111/麦当娜222/麦当娜333/麦当娜444/麦当娜555
					</view>
				</view>
				<view class="movie-oper" @click="praiseMe">
					<image src="../../static/tabBarIco/me_sel.png" class="praise-ico" mode=""></image>
					<view class="praise-me">点赞</view>
					<view :animation="animationData" class="praise-me animation-opacity">+1</view>
				</view>
			</view> -->
		</view>
		<!-- 猜你喜欢结束 -->
	</view>
</template>

<script>
	import common from '../../common/common.js'
	import helloComp from '../../components/helloComp.vue'
	import trailerStars from '../../components/trailerStars.vue'
	export default {
		data() {
			return {
				carouselList: [],
				moives: [1,2,3,4,5,6,7,8,9,10],
				hotSuperheroList: [],
				hotTraileroList: [],
				guessULikeList: [],
				
				animationData: {},
				animationDataArr: [
					{}, {}, {}, {}, {}
				]
			}
		},
		onPullDownRefresh() { // 监听用户下拉刷新的动作
			this.refresh()
		},
		onUnload() {
			// 页面卸载的时候清除动画数据
			this.animationData = {}
			this.animationDataArr = [{}, {}, {}, {}, {}]
		},
		onLoad() {
			// 条件编译语句
			// #ifdef APP-PLUS || MP-WEIXIN
			// 在页面创建的时候,创建一个临时的对象
			this.animation = uni.createAnimation()
			// #endif
			
			// 获取common.js中的服务器地址
			// let serverUrl = common.serverUrl
			
			// 通过挂载到全局
			let serverUrl = this.serverUrl
			
			// 请求轮播图数据
			uni.request({
				url: serverUrl + '/index/carousel/lists', //仅为示例，并非真实接口地址。
				method: 'POST',
				success: (res) => {
					console.log(res.data)
					// 获取真实数据之前判断状态是否为200
					if (res.data.data === 200) {
						let carouselList = res.data.data
						this.carouselList = carouselList
					}
				}
			})
			// 查询热门数据
			uni.request({
				url: serverUrl + '/index/movie/hot?type=superhero',
				method: 'POST',
				success: (res) => {
					console.log(res.data)
					// 获取真实数据之前判断状态是否为200
					if (res.data.data === 200) {
						let hotSuperheroList = res.data.data
						this.hotSuperheroList = hotSuperheroList
					}
				}
			});
			// 查询热门预告
			uni.request({
				url: serverUrl + '/index/movie/hot?type=trailer',
				method: 'POST',
				success: (res) => {
					console.log(res.data)
					// 获取真实数据之前判断状态是否为200
					if (res.data.data === 200) {
						let hotTraileroList = res.data.data
						this.hotTraileroList = hotTraileroList
					}
				}
			});
			this.refresh();
		},
		methods: {
			refresh() {
				uni.showLoading({
					mask: true
				});
				// uni.showNavigationBarLoading();
				
				
				// 查询猜你喜欢数据列表
				let serverUrl = this.serverUrl;
				uni.request({
					url: serverUrl + '/index/guessULike',
					method: 'POST',
					success: (res) => {
						if (res.data.data === 200) {
							let guessULikeList = res.data.data
							this.guessULikeList = guessULikeList
						}
					},
					complete: () => {
						// uni.hideNavigationBarLoading()
						uni.hideLoading();
						uni.stopPullDownRefreshOption();
					}
				})
			},
			// 实现点赞动画效果
			praiseMe(e) {
				// #ifdef APP-PLUS || MP-WEIXIN
				let gIndex = e.currentTarget.dataset.gindex
				console.log(gIndex)
				
				// 构建动画数据 并且通过step来表示这组动画的完成
				this.animation.translateY(-70).opacity(1).step({
					duration: 400
				})
				// 导出动画数据到view组件,实现组件的动画效果
				// this.animationData = this.animation.export()
				this.animationData = this.animation
				this.animationDataArr[gIndex] = this.animationData.export()
				// 还原动画
				setTimeout(function() {
					this.animation.translateY(0).opacity(0).step({
						duration: 0
					})
					// this.animationData = this.animation.export()
					this.animationData = this.animation
					this.animationDataArr[gIndex] = this.animationData.export()
				}.bind(this), 500)
				// #endif
			}
		},
		components: {
			helloComp,
			trailerStars
		}
	}
</script>

<style>
	@import url("./index.css")
</style>
