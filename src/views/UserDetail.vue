<template>
	<div class="container box">
		<div class="banner flex flex-center">
			<img :src="userVo.user.banner" class="cover shadow" />
			<div class="info m-1">
				<img :src="userVo.user.avatar" class="avatar " />
			
			
				<p class="t-1">{{ userVo.user.nickname }}</p>
				<!-- <p>{{ userVo.user.introduction.slice(0, 20) }}...</p> -->
			</div>
		</div>
		<div class="row t-2">
			<div class="col-8">
				<div class="col-12" v-for="(item, index) in userVo.articleList" :key="index">
					<div class="media-wraaper shadow ">
						<div class="media-left"><img :src="item.article.thumbnail" class="thumnail-xs" /></div>
						<div class="media-middle">
							<router-link :to="{ path: '/article/' + item.article.id }">
								<div class="subtitle">
									{{ item.article.title }}
								</div>
							</router-link>
							<p class="sub-title">{{ item.article.summary }}</p>
						</div>
						<div class="row-bt">
							<!-- <router-link :to="{ path: '/article/' + item.article.id }"><input type="button" value="编辑"></router-link> -->
							<input type="button" value="删除" @click="delate(item.article.id)"/>
							
						</div>
					</div>
					
				</div>
			</div>
			<div class="col-4">
				<div v-if="userVo.user.id==user.id">
					<div class="p-card">
						
						<router-link to="/Personal">
							<button type="info" plain class="p-bt">修改个人中心</button>
						</router-link>
						<div class="p-text">
							<p>昵称:{{userVo.user.nickname}}</p>
							<p>性别:{{userVo.user.gender}}</p>
							<p>地址:{{userVo.user.address}}</p>
							<p>简介:{{userVo.user.introduction}}</p>
							
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
			user: JSON.parse(localStorage.getItem('user')),
			userDto: {
								
					nickname:'',
					gender:'',
					address: '',
					introduction:'',
								
			},
			userVo: {
				user: {},
				articleList: {}
			}
		};
	},
	created() {
		var id = this.$route.params.id;
		this.axios.get(this.GLOBAL.baseUrl + '/user/' + id).then(res => {
			console.log(res.data.data);
			this.userVo = res.data.data;
		});
	},
	methods: {
		delate(articleid){
			this.axios({
				method:'delete',
				url:this.GLOBAL.baseUrl+'/article/' + articleid,
				data:JSON.stringify(this.articleid)
			}).then(res =>{
				if(res.data.msg ==='成功'){
					alert('已删除');
					this.$router.push();window.location.reload();
				}else{
					alert('失败');
				}
			});
			
		},
					upda(userDto) {
						this.axios({
							method: 'post',
							url: this.GLOBAL.baseUrl + '/user/change',
							data: JSON.stringify(this.userDto)
						}).then(res => {
							if (res.data.msg === '成功') {
								alert('更新成功');
								this.$router.push('');
							} else {
								alert(res.data.msg);
							}
						});
					}
	}
};
</script>

<style scoped="scoped">
.p-card{
	width: 100%;
	height: 400px;
	
	
}
.p-text{
	margin-left: 400px;
	height: 100px;
	font-size: 60px;
	
}
.p-bt{
	margin-left: 400px; 	
	height: 30px;
}
.banner {
	width: 100%;
	height: 300px;
}
.cover {
	width: 100%;
	height: 100%;
	border-radius: 10px;
}
.info {
	position: relative;
	top: -60px;
	left: -400px;
	color: #fff;
	margin-bottom: -50px;
	padding: 10px;
	background-color: rgb(0, 0, 0,);
	width: 130px;
	height: 130px;
	margin: 0 auto;
	text-align: center;
	border-radius: 20px;
}
.info img {
	width: 80px;
	height: 80px;
	border-radius: 50%;
	border: 2px solid #fff;
	margin-bottom: 10px;
}
.row {
	margin-top: -50px;
	width: 100%;
	
}
.row-bt{
	position: relative;
	top: 140px;
	
}
.row-bt input{
	margin-left: 5px;
}
.box{
	position: relative;
	
}
.m-1{
	position: absolute;
	top: 200px;
	left: 0px;
}
.t-1{
	position: relative;
	top: -90px;
	left: 70px;
}
.t-2{
	position: relative;
	top: 50px;
	left: -35px;
}
</style>
