<template>
	<div>
		<label>用户名：</label><input type="text" name="" v-model="user">
		<label>密码：</label><input type="password" name="" v-model="pwd">
    <mt-button @click=$router.go(-1)>返回</mt-button>
		<mt-button @click="login">登录</mt-button>
		<span @click="forget" class="forget">忘记密码</span>
	</div>
</template>

<script>
export default {

  name: 'login',

  data () {
    return {
    	user:'',
    	pwd:'',
    	sql:[]
    }
  },
  methods:{
    msg(msg){
      this.$toast({  
              message: msg, //提示内容
              position: 'center', //提示框位置
              duration: 2000 , //持续时间（毫秒），若为 -1 则不会自动关闭
          });
    },
  	login(){
      //console.log(this.sql)
  		for (var i = this.sql.length - 1; i >= 0; i--) {
  			if (this.sql[i].name==this.user && this.sql[i].pwd == this.pwd) {
  				this.$store.state.login = true
  				this.$store.state.user = this.user
          //console.log(this.$store.state.user)
          this.msg('登录成功！ ' + this.$store.state.user + '已登录')
  				this.$router.push({name:'home'})
  				return
  			}
      }
  				//console.log('账号或密码错误')
          this.msg('账号或密码错误') 
  				this.user = ''
  				this.pwd = ''
  				return 		
  	},
  	forget(){
  		this.$router.push({name:'reg'})
  	}
  },
  created(){
  	this.$axios.get('myapi/user')
  	.then(res=>{
  		this.sql = res.data
      console.log(sql)
  	})
  	.catch(err=>{
  		console.log(err)
  	})
  }
}
</script>

<style lang="css" scoped>
.forget{
	color: #55a;
	display: block;
	margin-right: 20px;
	font-size: 14px;
	text-align: right;
	text-decoration: underline;
}
</style>