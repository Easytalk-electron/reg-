<template>
  <div>
    <div class="qrcode_img">
      <img :src="qrcode" alt class="">
    </div>

    <div class="login-wrap" v-show="showLogin">
      <h3>登录</h3>
      <p v-show="showTishi">{{tishi}}</p>
      <input type="text" placeholder="请输入用户名" v-model="username">
      <input type="password" placeholder="请输入密码" v-model="password">
      <button v-on:click="login">登录</button>
      <span v-on:click="ToRegister">前往注册</span>
    </div>

    <div class="register-wrap" v-show="showRegister">
      <h3>注册</h3>
      <p v-show="showTishi">{{tishi}}</p>
      <input type="text" placeholder="请输入用户名" v-model="newUsername">
      <input type="password" placeholder="请输入密码" v-model="newPassword">
      <button v-on:click="register">注册</button>
      <span v-on:click="ToLogin">返回登录</span>
    </div>
  </div>
</template>

<script>
  import qrcode from "@/assets/qrcode.jpg";

  export default {
    data() {
      return {
        qrcode: qrcode,
        showLogin: true,
        showRegister: false,
        showTishi: false,
        tishi: '',
        username: '',
        password: '',
        newUsername: '',
        newPassword: ''
      }
    },
    methods:{
      ToRegister(){
        this.newUsername=''
        this.newPassword=''
        this.showRegister = true
        this.showLogin = false
      },
      ToLogin(){
        this.username=''
        this.password=''
        this.showRegister = false
        this.showLogin = true
      },
      register(){
        if(this.newUsername == "" || this.newPassword == ""){
          alert("请输入用户名或密码")
        }else{
          let sha256 = require("js-sha256").sha256;
          let sNewPassword = sha256(this.newPassword);
          let data = {'username':this.newUsername,'password':sNewPassword}
          this.$http.post('/register',data).then((res)=>{
            console.log(res)
            if(res.data == 1){
              this.tishi = "注册成功"
              this.showTishi = true
              this.username = ''
              this.password = ''

              this.showRegister = false
              this.showLogin = true
              this.showTishi = false

            }else {
              this.tishi = "用户名重复"
              this.showTishi = true
            }

          })
        }
      },
      login() {
        if (this.username == "" || this.password == "") {
          alert("请输入用户名或密码")
        } else {
          let sha256 = require("js-sha256").sha256;
          let sPassword = sha256(this.Password);

          let data = {'username': this.username, 'password': sPassword}

          this.$http.post('/login', data).then((res) => {
            console.log(res)
            if (res.data == -1) {
              this.tishi = "该用户不存在"
              this.showTishi = true
            } else if (res.data == 0) {
              this.tishi = "密码输入错误"
              this.showTishi = true
            }
            else {
              this.tishi = "登录成功"
              this.showTishi = true

              localStorage.setItem('userId',JSON.stringify(res.data));

              setTimeout(function(){
                this.$router.push('/main')
              }.bind(this),1000)
            }
          })
        }
      },

    }
  }
</script>

<style scoped lang="scss">
  .qrcode_img{margin-top: 100px; text-align: center;}
  .login-wrap{text-align:center; margin-top: 100px;}
  .register-wrap{text-align:center; margin-top: 100px;}
  h3{margin-bottom: 10px;}
  input{display:block; width:250px; height:40px; line-height:40px;  margin:0 auto;margin-bottom: 10px; outline:none; border:1px solid #888; padding:10px; box-sizing:border-box;}
  p{color:red;}
  button{display:block; width:250px; height:40px; line-height: 40px; margin:0 auto; border:none; background-color:#41b883; color:#fff; font-size:16px; margin-bottom:5px;}
  span{cursor:pointer;}
  span:hover{color:#41b883;}

</style>