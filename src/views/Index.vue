<template>
	<div class="box">
		<!-- <div class="row ">
			<div class="col-3" v-for="(item, index) in topics" :key="index">
				<div class="card link shadow">
					<router-link :to="{ path: '/topic/' + item.id }"><img :src="item.logo" class="logo" /></router-link>
					<p class="title">{{ item.topicName }}</p>
					<p class="sub-title">{{ item.description.slice(0, 20) }}...</p>
					<p class="meta">
						<span class="gutter">{{ item.articles }}篇文章,</span>
						<span>{{ item.follows }}人关注</span>
					</p>
				</div>
			</div>
		</div> -->

		<div class="row">
			<img src="../assets/img/222.jpg" class="imgg">
			
			<div class="col-8">
				<h3>热门文章</h3>
				<div v-for="(item, index) in articles" :key="index" class="col-12">
					<div class="media-wraaper border ">
						<!-- <div class="media-left">
							<router-link :to="{ path: '/user/' + item.article.userId }">
							<img :src="item.author.avatar" class="avatar-lg link" />
							</router-link>
							<p>{{ item.author.nickname }}</p>
							<strong>来自</strong>
							<p>{{ item.topic.topicName }}</p>
						</div> -->
						<div class="media-middle flex flex-around flex-left">
							<div class="text-box">
								<router-link :to="{ path: '/article/' + item.article.id }">
								<div class="subtitle">
									 {{ item.article.title }} 
								</div>
								</router-link>
								<p class="sub-title link">{{ item.article.summary }}</p>
							</div>
							
							<p>
								<span class="meta gutter"><i class="iconfont">&#xe60c;</i><span class="advance-btn">{{ item.article.comments }}</span></span>
								<span class="meta"><i class="iconfont">&#xe615;</i><span class="advance-btn">{{ item.article.likes }}</span></span>
							</p>
						</div>
						<div class="media-right "><img :src="item.article.thumbnail" alt="" class="text2" /></div>
					</div>
				</div>
			</div>
			<div class="col-4">
				<h3>热门作者</h3>
				<div v-for="(item, index) in users" :key="index" class="row" >
					<div class="col-12 border box-box">
						<div class="flex-center-y">
							<router-link :to="{ path: '/user/' + item.id }">
							<img :src="item.avatar" class="avatar-xs link" />
							</router-link>
							<p class="sub-title">{{ item.nickname }}</p>
						</div>
						<div class="flex-center-y">
							<p class="meta">{{ item.fans }}粉丝</p>
							<p class="meta">{{ item.articles }}篇文章</p>
						</div>
						<!-- <button v-if="book.isThumbUp!==true" class="btn"  @click="changeThumbUps(book)" >
								<i class="iconfont">&#xe644;</i>
								关注
						<tton>
						<button v-if="book.isThumbUp===true" class="btn1"  @click="changeThumbUps(book)" >
							<i class="iconfont">&#xe676;</i>
								已关注
						<tton> -->
						<div class="flex-center-y">
							
							
							
							<button v-if="isDao.isThumbUp!==true" class="btn btn-follow"  @click="changeThumbUps(isDao,item)">
								关注</button>
							<button v-if="isDao.isThumbUp===true" class="btn btn-follow"  @click="changeThumbUps(isDao,item)">
								已关注</button>
								<!-- :class="{'btn-follow':item.isThumbUp!==true}" -->
							</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			articles: [],
			users: [],
			topics: [],
			isDao:{
				"isThumbUp": true,
			}
			
		};
	},
	created() {
		this.axios.get(this.GLOBAL.baseUrl + '/article').then(res => {
			// console.log(res.data.data);
			this.articles = res.data.data;
		});
		this.axios.get(this.GLOBAL.baseUrl + '/user').then(res => {
			// console.log(res.data.data);
			this.users = res.data.data;
		});
		this.axios.get(this.GLOBAL.baseUrl + '/topic').then(res => {
			// console.log(res.data.data);
			this.topics = res.data.data;
		});
	},
	methods: {
		changeThumbUps(isDao) {
			if (isDao.isThumbUp == true) {
				isDao.isThumbUp = false
				// item.thumbUpCount--
			} else {
				isDao.isThumbUp = true
				// item.thumbUpCount++
			}
		},
		// chan(item,isDao){
		// 	isDao.isThumbUp=item.status
		// }
		
	}
};
</script>

<style scoped="scoped">
.logo {
	border-top-left-radius: 5px;
	border-top-right-radius: 5px;
}
.logo:hover {
	opacity: 0.6;
}
.imgg{
	width: 100%;
	height: 200px;
}
.text-box{
	height:100px;
	width: 100%;
}
.box-box {
	display: flex;
	justify-content: space-around;
	height: 70px;
	/* padding: 10px; */
}
.text2{
	height: 100%;
}
</style>
