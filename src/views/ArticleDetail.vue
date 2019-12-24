<template>
	<div class="container border ">
		<h2 class="title">{{ articleVo.article.title }}</h2>
		<div class="box1 ">
			<!-- <img :src="articleVo.author.avatar" class="avatar-xs" /> -->
			<router-link :to="{ path: '/user/' + articleVo.article.userId }">
			<img :src="articleVo.author.avatar" class="avatar-lg link" />
			</router-link>
			<span class="meta gutter">{{ articleVo.author.nickname }}</span>
			<span class="meta gutter">
				{{ articleVo.article.createTime.date.year }}年{{ articleVo.article.createTime.date.month }}月{{ articleVo.article.createTime.date.day }}日 {{ articleVo.article.createTime.time.hour }}:{{
					articleVo.article.createTime.time.minute
				}}:{{ articleVo.article.createTime.time.second }}
			</span>
		</div>
		
		
	<div class="first">
		<div class="first-1">
			<div v-html="articleVo.article.content" class="box-top1"></div>
		</div>
		<div class="first-2">
			<div class="row1 ">
				<div ><input type="text" v-model="commentDto.content">
					<button type="button" class="bl-btn" @click="comment(commentDto)">添加评论</button>
					<p type="text" v-model="commentDto.userId=user.id">
					<p type="text" v-model="commentDto.articleId=articleVo.article.id">
					<p>评论:</p>
					<hr>
					
					
					<div v-for="(com, index) in comments" :key="index">
						<img src="user.avatar" />
						<span>{{user.nickname}}  的评论</span>
						
						<div class="card-1">
							<p>{{com.content}}</p>
						</div>
						<button v-if="user.id==com.userId"  @click="comdelete(com.id)">删除评论</button></div>
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
				articleVo: {},
				user: JSON.parse(localStorage.getItem('user')),
				articles: [],
				comments:[],
				likes:[],
				user_id: "",
				like_content: "收藏",
				deleteid:'',
				id:'',
				id1: null,
				istrue: false,
				articleAddDto: {
					userId: '',
					topicId: '',
					content: '',
					title: '',
					summary: ''
				},
				articleDto: {
					title: '',
					summary:'',
					content:'',
					id:'',
					
				},
				commentDto:{
					content:'',
				
				},
				commentDtos:{
					content:'',
					id:'',
				}
			};
		},
		created() {
			var number = Math.ceil(Math.random() * 10);
			var id = this.$route.params.id;
			var user = JSON.parse(localStorage.getItem("user"));
			this.id1=this.$route.params.id1;
			// commentDtos.id=comments.id;
			this.user_id = user.id;
			this.axios.get(this.GLOBAL.baseUrl + '/article/' + id).then(res => {
				console.log(res.data.data);
				this.articleVo = res.data.data;
				this.getcom(id)
			});
			this.axios.get(this.GLOBAL.baseUrl + '/article').then(res => {
				this.articles = res.data.data;
			});

			
		},
		computed: {},
		methods: {
			getcom(id){
				this.axios.get(this.GLOBAL.baseUrl + '/comment',{
					
					params:{
						
						"id":id,
					}
				}).then(res => {
					this.comments=res.data.data;
				});
			},
			stop() {
				this.istrue = true
			},
			go() {
				this.istrue = false
			},

			comment(commentDto){
				this.axios({
					method:'post',
					url:this.GLOBAL.baseUrl+'/comment',
					data:JSON.stringify(this.commentDto)
				}).then(res=>{
					// alert(111)
					if(res.data.msg==='成功'){
						alert('评论成功');
						window.location.reload();
					}else{
						alert(res.data.msg);
					}
				})
			},
			comdelete(id){
				this.axios({
					method:'delete',
					url:this.GLOBAL.baseUrl+'/comment/' + id,
				}).then(res=>{
					// console.log(res)
					// alert(222)
					// alert(res.msg);
					window.location.reload();
					if(res.data.msg==='成功'){
						alert('删除成功');
						window.location.reload();
					}else{
						alert(res.data.msg);
					}
					
				})
			},


			
		}
	};
</script>

<style scoped="scoped">
	.first{
		
		display: flex;
	}
	.first-1{
		flex: 0 0 83%;
	}
	.first-2{
		flex:  0 0 20%;
	}
	.box1{
		height: 50px;
		line-height: 50px;
	}
	.box-top1{
		margin-top: 20px;
	}
	.row1{
		background-color: rgb(0, 0, 0,0.1);
		width: 259px;
		height: 600px;
	}
	.row-top1{
		margin-top: 0px;
		margin-left: 83%;
	}
	
</style>
