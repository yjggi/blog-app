<template>
	<div>
		<div class="nav primary-fill shadow">
			<div class="nav-bar nav-list">
				
				<ul class=" flex-around bl-df-start">
					<li class="nav-item"><router-link to="/index">主页</router-link></li>
					<li class="nav-item"><router-link to="/topics">专题</router-link></li>
					<li class="nav-item"><router-link to="/articles">文章</router-link></li>
					<li class="nav-item"><router-link to="/users">作者</router-link></li>
					<li class="nav-item"><router-link to="/issue">发文章</router-link></li>
				</ul>
				<ul class="bl-df-left box-left">
					<li class="nav-item"><input type="text" class="input-box" placeholder="请输入搜索内容" v-model="keywords" /></li>
					<li class="nav-item"><i class="iconfont2 bt3" @click="search">&#xe602;</i></li>
					<!-- <button class="btn btn-lg btn-rd dark-border warning-fill" @click="search">搜索</button> -->
				</ul>
				<ul class="bl-df-left box-right">
					<li class="nav-item box-text" v-if="!this.user"><router-link to="/sign-in">登录</router-link></li>
						<router-link :to="{ path: '/user/' + user.id }" v-if="this.user"><img :src="user.avatar" @mouseenter="this.show = true" class="avatar-xs " /></router-link>
					<li class="nav-item" v-if="this.user"><a class="link bt" @click="logout"><i class="iconfont1">&#xe60b;</i></a></li>
				</ul>
			</div>
		</div>
		<router-view class="container" />
	</div>
</template>
<script>
export default {
	data() {
		return {
			user: JSON.parse(localStorage.getItem('user')),
			keywords: ''
		};
	},
	created() {},
	methods: {
		logout() {
			this.user = null;
			localStorage.clear();
		},
		search() {
			let currentPath = this.$route.path;
			alert(currentPath);
			if (currentPath != '/search' || currentPath != '/search/article' || currentPath != '/search/topic' || currentPath != '/search/usere') {
				this.$router.push({ path: '/search', query: { keywords: this.keywords } });
			} else {
				this.$router.push({ path: '/empty', query: { keywords: this.keywords } });
			}
		}
	}
};
</script>
<style scoped>
a:hover{
	color: rgb(141, 197, 242);
}
/* 路由激活高亮样式 */
.router-link-active {
	background-color: rgba(141, 197, 242,0.5);
	font-weight: 700;
}
.container {
	margin-top: 80px;
}
.box-right{
	position: relative;
	left: 80px;
}
.box-text{
	position: relative;
	left: -50px;
}
.bt{
	position: relative;
	top: 20px;
	left: -30px;
}
.bt3{
	position: relative;
	top: -2px;
	left: 2px;
	cursor: pointer;
}

</style>
