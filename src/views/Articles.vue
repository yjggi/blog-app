<template>
	<div class="row">
		<div v-for="(item, index) in articles" :key="index" class="col-12 position2">
			<div class="media-wraaper bg shadow ">
				
				<div class="media-left"><img :src="item.article.thumbnail" /></div>
				
				<div class="media-middle flex flex-left">
					<router-link :to="{ path: '/article/' + item.article.id }">
						<div class="subtitle h-text">
							<!-- <span>{{ item.article.id }}</span> -->
							<span >  {{ item.article.title }}</span>
						</div>
					</router-link>
							
							
					
					<p class="sub-title link">{{ item.article.summary }}</p>
					<p>
						<span class="meta gutter"><i class="iconfont">&#xe60c;</i><span class="advance-btn">{{ item.article.comments }}</span></span>
						<span class="meta"><i class="iconfont">&#xe615;</i><span class="advance-btn">{{ item.article.likes }}</span></span>
					</p>
				</div>
				
			</div>
		</div>
		<div class="col-12"><button class="btn btn-lg btn-rd warning-fill position1" @click="loadMore">点击加载更多</button></div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			articles: [],
			currentPage: 1,
			count: 20
		};
	},
	created() {
		this.axios
			.get(this.GLOBAL.baseUrl + '/article', {
				params: {
					page: this.currentPage,
					count: this.count
				}
			})
			.then(res => {
				console.log(res.data.data.length);
				this.articles = res.data.data;
			});
	},
	methods: {
		loadMore() {
			this.currentPage = this.currentPage + 1;
			this.axios
				.get(this.GLOBAL.baseUrl + '/article', {
					params: {
						page: this.currentPage,
						count: this.count
					}
				})
				.then(res => {
					console.log(res.data.data.length);
					let temp = [];
					temp = res.data.data;
					for (var i = 0; i < temp.length; i++) {
						this.articles.splice(this.currentPage * this.count, 0, temp[i]);
					}
					console.log(this.articles.length);
				});
		}
	}
};
</script>

<style scoped="scoped">
.text-center{
	text-align: center;
}
.bg {
	background-image: url(../assets/img/article.png);
	background-size: contain;
	background-position-y: 100px;
}
.position2{
	position: relative;
	left: 100px;
}
</style>
