<template>
	<div class="row">
		<div v-for="(item, index) in articles" :key="index" class="col-12">
			<div class="media-wraaper bg shadow">
				<div class="media-left">
					<router-link :to="{ path: '/user/' + item.article.userId }">
					<img :src="item.author.avatar" class="avatar-lg link" />
					</router-link>
					<p>{{ item.author.nickname }}</p>
					<strong>来自</strong>
					<p>{{ item.topic.topicName }}</p>
				</div>
				<div class="media-middle flex flex-left">
					<router-link :to="{ path: '/article/' + item.article.id }">
						<p>
							<span>{{ item.article.id }}</span>
							{{ item.article.title }}
						</p>
					</router-link>
					<p class="sub-title link">{{ item.article.summary }}</p>
					<p>
						<span class="meta gutter"><i class="iconfont">&#xe60c;</i><span class="advance-btn">{{ item.article.comments }}</span></span>
						<span class="meta"><i class="iconfont">&#xe615;</i><span class="advance-btn">{{ item.article.likes }}</span></span>
					</p>
				</div>
				<div class="media-right"><img :src="item.article.thumbnail" /></div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			articles: [],
			keywords: ''
		};
	},
	created() {
		this.keywords = this.$route.query.keywords;
		console.log(this.keywords);
		this.axios
			.get(this.GLOBAL.baseUrl + '/article', {
				params: {
					keywords: this.keywords
				}
			})
			.then(res => {
				console.log(res.data.data.length);
				this.articles = res.data.data;
			});
	},
	methods: {}
};
</script>
<style></style>
