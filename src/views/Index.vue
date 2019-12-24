<template>
	<div class="box">
		
		<div class="row">
			<img src="../assets/img/12345.png" class="imgg">
			
			<div class="col-8 ">
				<h3>热门文章</h3>
				<div v-for="(item, index) in articles" :key="index" class="col-12 ">
					
					<div class="media-wraaper border shadow d-box">
						
						<div class="media-left "><img :src="item.article.thumbnail" alt="" class="text2 h-img" /></div>
						
						<div class="media-middle flex flex-around flex-right ">
							<div class="text-box">
								<router-link :to="{ path: '/article/' + item.article.id }">
								<div class="subtitle">
									<p class=" h-text"> {{ item.article.title }} </p>
								</div>
								</router-link>
								<p class="sub-title link c-color">{{ item.article.summary }}</p>
							</div>
							
							<p>
								<span class="meta gutter"><i class="iconfont">&#xe60c;</i><span class="advance-btn">{{ item.article.comments }}</span></span>
								<span class="meta"><i class="iconfont">&#xe615;</i><span class="advance-btn">{{ item.article.likes }}</span></span>
							</p>
						</div>
						
					</div>
				</div>
			</div>
			<div class="col-4">
				<h3>热门作者</h3>
				<div v-for="(item, index) in users" :key="index" class="row" >
					<div class="col-12 border box-box shadow">
						<div class="flex-center-y">
							<router-link :to="{ path: '/user/' + item.id }">
							<img :src="item.avatar" class="avatar-xs link h-img" />
							</router-link>
							<p class="sub-title">{{ item.nickname }}</p>
						</div>
						<div class="flex-center-y m-2">
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
							
							
						
							<!-- <button v-if="isDao.isThumbUp!==true" class="btn btn-follow"  @click="changeThumbUps(isDao,item)">
								关注</button>
							<button v-if="isDao.isThumbUp===true" class="btn btn-follow"  @click="changeThumbUps(isDao,item)">
								已关注</button> -->
						</div>
					</div>
					
				</div>
				<div v-for="(text, index) in List" :key="index" class="row m-1" >
					<div class="col-12  box-box ">
						<div class="flex-center-y">
							
							
						
							<button v-if="text.ist!==true" class="btn btn-follow"  @click="changeThumbUps(text)">
								关注</button>
							<button v-if="text.ist===true" class="btn btn-follow"  @click="changeThumbUps(text)">
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
			articles: [{}],
			users: [],
			topics: [],
			isDao:{
				"isThumbUp": true
			},
			List:[
				{
					"id":1,
					"ist":false
				},
				{
					"id":2,
					"ist":true
				},
				{
					"id":3,
					"ist":false
				},
				{
					"id":4,
					"ist":true
				},
				{
					"id":5,
					"ist":true
				},
				{
					"id":6,
					"ist":false
				},
				{
					"id":7,
					"ist":false
				},
				{
					"id":8,
					"ist":true
				},
				{
					"id":9,
					"ist":false
				},
				{
					"id":10,
					"ist":true
				},
			]
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
		changeThumbUps(text) {
			if (text.ist == true) {
				text.ist = false
			} else {
				text.ist = true
			}
		},
	}
};
</script>

<style scoped="scoped">
	.d-box{
		margin-top: 32px;
	}
	
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
	/* border: 10px solid #000000; */
}
.text2{
	height: 100%;
}
.m-1{
	position: relative;
	top: -1100px;
	left: 100px;
}
.m-2{
	position: relative;
	left: -30px;
}
.btn:hover{
	box-shadow: 0px 0px 3px #000;
}

/* rgb(141, 197, 242) */
/* .border{
	
	background-color: #00FF7F;
} */
</style>
