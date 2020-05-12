<template name="trailerStars">
	<view class="movie-score-wapper">
		<!-- <image src="../static/tabBarIco/index_sel.png" class="star-ico"></image>
		<image src="../static/tabBarIco/index_sel.png" class="star-ico"></image>
		<image src="../static/tabBarIco/index_sel.png" class="star-ico"></image>
		<image src="../static/tabBarIco/index_sel.png" class="star-ico"></image>
		<image src="../static/tabBarIco/index.png" class="star-ico"></image>
		<view class="movie-score">9.1</view> -->
		<image
			 v-for="yellow in yellowScore"
			 src="../static/tabBarIco/index_sel.png" 
			 class="star-ico"
	    ></image>
		<image 
			v-for="gray in grayScore"
			src="../static/tabBarIco/index.png" 
			class="star-ico"
		></image>
		<view class="movie-score" v-if="showNum == 1">{{innerScore}}</view>
	</view>
</template>

<script>
	export default {
		name: 'trailerStars',
		props: {
			innerScore: 0, // 定义外部传入的分数
			showNum: 0 // 是否需要显示具体的分数   1:显示    0:不显示
		},
		data() {
			return {
				yellowScore: 0,
				grayScore: 5
			}
		},
		// 生命周期 组件创建完成后被调用
		created() {
			var tempScore = 0
			if (this.innerScore != null && this.innerScore != undefined && this.innerScore != '') {
				tempScore = this.innerScore
			}
			
			var yellowScore = parseInt(tempScore / 2)
			var grayScore = 5 - yellowScore
			
			this.yellowScore = yellowScore
			this.grayScore = grayScore
			
		}
	}
</script>

<style>
.movie-score-wapper {
	display: flex;
	flex-direction: row;
}
.star-ico {
	width: 20upx;
	height: 20upx;
	margin-top: 6upx;
}
.movie-score {
	font-size: 16px;
	color: grey;
	margin-left: 8upx;
}
</style>
