<template>
	<div class="bl-container bl-df-jcenter con-img background-m">
		<div class="bl-col-8 left">
			<div msgborder class="say-box">
				<input type="hidden"  v-model="articleDao.userId=user.id" class="borderwrite"/>
				<input type="text" v-model="articleDao.title" class="border" msgborder placeholder="标题"/>
				<br>
				<br>
				<textarea class="say-box2" msgborder placeholder="这里是简介" type="text" v-model="articleDao.summary" ></textarea>
				
				<textarea class="say-box2" msgborder placeholder="这里是图片" type="text" v-model="articleDao.thumbnail" ></textarea>
				<textarea class="say-box1" msgborder placeholder="这里是内容" type="text" v-model="articleDao.content" ></textarea>
				<input msgboard type="button"  value="发送" @click="connect(articleDao)" class="btn-n"/>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		data(){
			return {
				user: JSON.parse(localStorage.getItem('user')),
				articles: [],
				istrue:false,
				articleDao: {
				 	userId:'',
					//用户id
					content:'',
					//内容
					title:'',
					//标题
					summary:'',
					//内容概括
					thumbnail:''
					//图片
				},
			}
		},
		created() {
			this.axios.get(this.GLOBAL.baseUrl + '/article').then(res => {
				 console.log(res.data.data);
				this.articles = res.data.data;
			});
		},
			methods:{
				connect(articleDao) {
					this.axios({
						method: 'post',
						url: this.GLOBAL.baseUrl+'/article',
						data: JSON.stringify(this.articleDao)
					}).then(res => {
						if (res.data.msg === '成功') {
							alert('发布成功');
						} else {
							alert(res.data.msg);
						}
					});
					// window.location.reload();
				}
			}
	}
</script>
<style>
	.page .btn-bg {
	    background: #c6eaf5!important;
	}
	.page button {
	    cursor: not-allowed;
	}
	.page .changebtn {
	    width: 30px;
	}
	.page button {
	    color: #646464;
	    border: 1px solid #85b9c8;
	    border-radius: 3px;
	    cursor: pointer;
	    background: #fff;
	    display: inline-block;
	    width: 30px;
	    height: 28px;
	    margin: 2px;
	    outline: none;
	}
	.page {
	    display: -webkit-box;
	    display: -ms-flexbox;
	    display: flex;
	    -ms-flex-wrap: wrap;
	    flex-wrap: wrap;
	    -webkit-box-pack: center;
	    -ms-flex-pack: center;
	    justify-content: center;
	    margin-top: 5px;
	}
	.triangle-bg {
	    width: 0;
	    height: 0;
	    border-width: 12px;
	    border-color: transparent #faf7f7 transparent transparent;
	    border-style: solid;
	    margin-left: -23px;
	    margin-right: -2px;
	    position: relative;
	    z-index: 3;
	}
	.triangle-line {
	    width: 0;
	    height: 0;
	    border-width: 13px;
	    border-color: transparent #647155 transparent transparent;
	    border-style: solid;
	    position: relative;
	    z-index: 2;
	}
	.board-content-details {
	    display: -webkit-box;
	    display: -ms-flexbox;
	    display: flex;
	    -webkit-box-pack: end;
	    -ms-flex-pack: end;
	    justify-content: flex-end;
	    -webkit-box-align: center;
	    -ms-flex-align: center;
	    align-items: center;
	    font-family: \\5FAE\8F6F\96C5\9ED1;
	    font-size: 12px;
	}
	.board-content {
	    -webkit-box-sizing: border-box;
	    box-sizing: border-box;
	    -ms-flex-negative: 1;
	    flex-shrink: 1;
	    width: 100%;
	    border: 1px solid #647155;
	    border-radius: 10px;
	    padding: 10px;
	    -webkit-box-shadow: 0 0 5px rgba(0,0,0,.4);
	    box-shadow: 0 0 5px rgba(0,0,0,.4);
	}
	.board-item pre {
	    font-family: Arial;
	    white-space: pre-wrap;
	    word-wrap: break-word;
	}
	.board-content-s {
	    margin-left: 15px;
	}
	.profile-pic img {
	    width: 45px;
	    height: 45px;
	}
	.msg-leaver {
	    display: -webkit-box;
	    display: -ms-flexbox;
	    display: flex;
	    -webkit-box-align: center;
	    -ms-flex-align: center;
	    align-items: center;
	}
	.board-item {
	    font-family: FangSong;
	    -webkit-box-sizing: border-box;
	    box-sizing: border-box;
	    padding: 5px 10px;
	    width: 100%;
	}
	.leavemsg {
	    margin-top: 32px;
	}
	.btn-n{
		width: 100px;
		height: 34px;
		outline: none;
		border: 1px solid #08D;
		color: #fff;
		padding:0 32px;
		text-align: center;
		font-size: 14px;
		border-radius: 10px;
	    background-color: rgb(74, 138, 244);
		margin-top: 10px;
		margin-left: 545px;
		cursor: pointer;
	}
	.shade{
		background-color: rgb(0, 121, 215);
	}
	.bottom-col{
		
	}
	
	.exit-aite {
	    margin-left: 5px;
	    color: #5bc0de;
	    cursor: pointer;
	}
	.msgboard {
	    background: #faf7f7;
	    margin-top: 10px;
	    padding: 20px 10px;
	    border-radius: 5px;
	    font-size: 14px;
	    color: #404040;
		}
	.say-box{
		margin: 10px 10px 5px;
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
	    width: 100%;
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

	a, a:link {
		font-weight:bold;
	    color:rbg(26, 160, 52);
	    text-decoration: none;
		
	}
	
	/* 边框 */
	.borderwrite {
		border: 1px solid #ddd;
		height: 100px;
		align-items: center;
		border-radius: 5px;
	}
	
	/* 下边框 */
	.border-bottom {
		border-bottom: 1px solid #ddd;
		padding-bottom: 20px;
	}
</style>
