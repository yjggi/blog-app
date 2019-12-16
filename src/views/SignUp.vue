<template>
	<div id="bg">
		<div class="header">
						
					<img src="../assets/img/header.jpg" >
					<!-- https://s1.hdslb.com/bfs/static/passport/static/img/loadTV.99606e2.gif -->
			</div>
			<img src="https://s1.hdslb.com/bfs/static/passport/static/img/loadTV.99606e2.gif" class="tv-img">
				<div class="container">
					
					<div class="head">
						
						<span class="tab-item"><router-link to="/sign-in">登录</router-link></span>
						<span class="tab-item"><router-link to="/sign-up">注册</router-link></span>
						
					</div>
					
					<div class="box">
						
						<div class="left">
							
							<div class="pp">
								<p>扫码登录</p>
								<p>或扫码下载APP</p>
							</div>
							<div class="ee"><img src="../assets/img/1111.png"></div>
							
							<div>
								<img src="https://s1.hdslb.com/bfs/static/passport/static/img/2233login.af9c53d.png" >
							</div>
						</div>
						
						
						 <form class="right">
							<!-- <div class="tab-box" v-if="show&&selected===0">
								<div class="right-body">
									
									<input type="text"  placeholder="你的手机号／邮箱" class="text-input" v-model="userDto.mobile" id="mobile"/>
									
									<input type="password"   placeholder="密码" class="text-input" v-model="userDto.password"/>
									<div>
										<input type="text" class="right-body-input" placeholder="请输入验证码" v-model="userDto.code"/>
									
										<img class="verify" @click.prevent="refresh" ref="codeImg" />
									</div>
									
									
									<div style="display: flex; align-items: center;">
										<input type="checkbox">
										<span style="margin-left: 5px; font-size: 12px; color: #000000;" >记住我(不是自己的电脑上不要勾选此项)</span>
									</div>
									
									<input type="button" value="登录" class="text-input" @click="signIn(userDto)"/>
								</div>
							</div>	 -->
							
							
							
							<div class="tab-box">	
							<!-- <div class="tab-box" > -->
								<div class="right-body2">
									<input type="text"  placeholder="填写常用手机号" class="text-input" v-model="userDto.mobile" id="mobile"/>
									
									<input type="password"   placeholder="密码(6到16个字符组成,区分大小写)" class="text-input" v-model="userDto.password" />
									
									
									<div style="display: flex; align-items: center;">
										<input type="checkbox">
										<span style="margin-left: 5px; font-size: 12px; color: #000000;" >我已同意《哔哩哔哩弹幕网用户使用协议》</span>
									</div>
									<!-- <div>
										<input type="text" class="right-body-input" placeholder="请输入验证码" v-model="userDto.code"/>
										<img class="verify" @click.prevent="refresh" ref="codeImg" />
									</div> -->
									<input type="button" class="text-input" value="注册" @click="signUp(userDto)" />
								</div>
							</div>
						</form> 
						
					</div>
				
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			userDto: {
				mobile: '',
				password: ''
			}
		};
	},
	created() {
		var number = Math.ceil(Math.random() * 10);
		this.codeUrl = this.GLOBAL.baseUrl + '/code?num = ' + number;
	},
	methods: {
		signUp(userDto) {
			this.axios({
				method: 'post',
				url: this.GLOBAL.baseUrl + '/user/sign-up',
				data: JSON.stringify(this.userDto)
			}).then(res => {
				if (res.data.msg === '成功') {
					alert('注册成功');
					this.$router.push('/sign-in');
				} else {
					alert(res.data.msg);
				}
			});
		}
	}
};
</script>
<style scoped>
/* #bg {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background-image: url(../assets/img/topic.png);
	} */
	*{
		margin: 0;
		padding: 0;
	}
	/* body{
		background-color: #00BBDD;
	} */
	.verify {
		flex: 0 0 50%;
		height: 40px;
		margin-top: 20px;
	}
	.container{
		display: block;
		height: 660px;
		width: 60%;
		margin: 0 auto;
		/* text-align: center; */
		justify-content: center;
		/* align-items: center; */
		margin-top: -70px;
		
		
	}
	
	.tab-item {
		cursor: pointer;
		margin-right: 10px;
		flex: 0 0 80px;
		text-align: center;
		line-height: 38px;
	}
	
	.active {
		color: #00BBDD;
		font-weight: 600;
		border-bottom: 2px solid #00BBDD;
	}
	.tab-box{
		
		line-height:50px;
		
		height: 300px;
		
		
		color: #eee;
		/* margin-top: -20px; */
	}
	.box{
		display: flex;
		
		width:100%
	}
	
	.head{				
		width: 100%;
		height: 60px;
		background-color: #FFFFFF;					
		text-align: center;	
		font-size: 40px;
		position: relative;
		right: -10px;
		/* margin-top: -80px; */
		
	}
	
	.left{
		flex: 0 0 48%;
		float: left;
		position: relative;
		top:-10px;
		right: 20px;
		border-right: 1px solid #000000;
		border-top: 1px solid #000000;
		margin-top:-10px;
		position: relative;
		top: 10px;
	}
	.right{
		flex: 0 0 48%;
		float: left;
		border-top: 1px solid #000000;
		/* margin-top:-10px;
		/* background-color: #4169E1; */
		margin-left: -20px;
	}
	
	
	.header{
		background-color: rgb(0, 160, 216);
		text-align: center;
		height: 86px;
	}
	
	/* 二维码 */
	.ee img{
		height: 30%;
		width: 30%;
		position: relative;
		right: -170px;
		
	}
	/* 小电视 */
	.tv-img{
		position: relative;
		top: -10px;
		left: 260px;
		/* 优先级 */
		z-index: 100;
	}
	/* 文字 */
	
	.pp p{
		text-align: center;
		position: relative;
		top: 250px;
		left: 2px;
	}
	.right-body-input{
		width: 150px;
		height: 30px;
		margin-left: 20px;
		position: relative;
		top: -10px;
	}
	.right-body{
		width: 80%;
		padding-top: 40px;
		margin: 0 auto;
		height: 100%;
	}
	.right-body img{
		width: 90px;
		height: 30px;
		margin-left: 20px;
		pointer:relative;
		top: 120px;
	}
	.right-body2{
		width: 80%;
		padding-top: 20px;
		margin: 0 auto;
		height: 100%;
		
		
	}
	.right-body2 img{
		width: 90px;
		height: 30px;
		margin-left: 20px;
	}
	.right-body input{
		border-radius:5px;
		border-width: 1px;
	}
	.text-input{
		font-size: 18px;
		
		width:100%;
		height: 40px;
		margin-top:20px;
	}
	.register{
		text-align: center;
		width: 100%;
		height: 40px;
	}
	.btn{
		width: 120px;
		height: 30px;
		outline: none;
		border: none;
		text-align: center;
		font-size: 14px;
		border-radius: 10px;
	}
	.btn-normal {
		background-color: rgb(0, 160, 216);
		color: #fff;
	}
	
	.btnDisabled {
		background-color: #ddd;
		color: #333;
	}
	/* .kk{
		font-size: 18px;
		
		width:100%;
		height: 40px;
		margin-top:20px;
		pointer-events: none;
		cursor: default;
		opacity: 0.6;
	} */
</style>
