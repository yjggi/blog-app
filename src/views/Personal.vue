<template>
	<div class="container box ">
		<div class="ip">
			<input type="hidden"  v-model="userDto.id=user.id" class="say-box2" />
			<p>昵称:</p>
			<input class="say-box2" type="nickname" v-model="userDto.nickname=user.nickname" >
			<p>性别：</p>
			<input class="say-box2" type="gender" v-model="userDto.gender=user.gender" />
			<p>地址:</p>
			<input class="say-box2" type="address" v-model="userDto.address=user.address">
			<p>简介:</p>
			<input class="say-box2" type="introduction" v-model="userDto.introduction=user.introduction" />
			<p class="p-top"> <button type="button" class="bl-btn" @click="upda(userDto)">修改</button></p>
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
	.ip input{
		margin-top: 10px;
	}
	.ip p{
		margin-top: 25px;
	}
	.p-top{
		position: relative;
		top: 10px;
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
	top: 240px;
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
.say-box{
		margin: 10px 10px 5px;
		text-align: center;
		position: relative;
		top: 300px;
		left: -150px;
	}
	.say-box1 {
	    font-family: STFangsong;
	    resize: none;
	    overflow-y: none;
	    outline: none;
	    font-size: 14px;
	    padding: 5px;
	    border: none;
	    border-radius: 6px;
	    -webkit-box-sizing: border-box;
	    box-sizing: border-box;
	    width: 60%;
	    height: 100px;
	    -webkit-box-shadow: 0 0 8px rgba(0,0,0,.4);
	    box-shadow: 0 0 8px rgba(0,0,0,.4);
	}
	
	.say-box2 {
	    font-family: STFangsong;
	    resize: none;
	    overflow-y: none;
	    outline: none;
	    font-size: 14px;
	    padding: 5px;
	    border: none;
	    border-radius: 6px;
	    -webkit-box-sizing: border-box;
	    box-sizing: border-box;
	    width: 60%;
	    height: 40px;
	    -webkit-box-shadow: 0 0 8px rgba(0,0,0,.4);
	    box-shadow: 0 0 8px rgba(0,0,0,.4);
	}
</style>

