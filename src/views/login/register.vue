
<template>
  <el-container class="login-container">
       
    <div style="margin: 0 auto; width:400px;">
      
      <el-form ref="loginForm" :label-position="labelPosition" label-width="80px" :model="formLabelAlign">
        <el-form-item label="账号" prop="username">
          <el-input v-model="formLabelAlign.username"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="password">
          <el-input v-model="formLabelAlign.password"></el-input>
        </el-form-item>
        <el-form-item label="昵称" prop="name">
          <el-input v-model="formLabelAlign.name"></el-input>
        </el-form-item>
        <el-button :loading="loading"  type="primary" @click="handleLogin()">注册</el-button>
        <p>已有账号？<a @click.prevent.stop="toLogin">登录</a></p>
      </el-form>
    </div>
  </el-container>
</template>

<script >
/* 按需导入 */
import {validUsername} from "../../utils/validate.js"

export default {
  name:'Login',
  data() {
    //data里面可以写函数
    const validateUsername=(rule,value,callback)=>{
        if(value===""){
            
            return callback(new Error("用户名不能为空"))
        }
    }
    const validatePassword=(rule,value,callback)=>{
        if(value===""){
            return callback(new Error("密码不能为空"))
        }
    }
    const validatename=(rule,value,callback)=>{
        if(value===""){
            
            return callback(new Error("昵称不能为空"))
        }
    }
    return {
      labelPosition: "right",
      formLabelAlign: {
        username: " ",
        password: "",
        name:""
      },
      loading:false,
    };
  },
  mounted(){
    
 
  },
  methods:{
        handleLogin(){
            this.$refs.loginForm.validate(valid=>{
                if(valid){
                  this.loading=true;
                  console.log(this.formLabelAlign,"this.formLabelAlig")
                  this.$store.dispatch("RegisterByUser",this.formLabelAlign).then(()=>{
                    this.loading = false;
                    this.$router.push({path:this.redirect || "/"})
                  })
                  /* this.$store.dispatch('LoginByUsername', this.formLabelAlign).then(()=>{
                    this.loading=false;
                    this.$router.push({path:this.redirect || "/"})
                  }) */
                  
                }else{
                    console.log("erro sumbmit!!!!")
                    return false
                }
            })
        },
        toLogin(){
            this.$emit("changestaus","login")
         }
  },
};
</script>
<style rel="stylesheet/scss" lang="scss">
  /* 修复input 背景不协调 和光标变色 */
  /* Detail see https://github.com/PanJiaChen/vue-element-admin/pull/927 */

  $bg:#283443;
  $light_gray:#eee;
  $cursor: #fff;

  @supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
    .login-container .el-input input{
      color: $cursor;
      &::first-line {
        color: $light_gray;
      }
    }
  }

  /* reset element-ui css */
  .login-container {
    .el-input {
      display: inline-block;
      height: 47px;
      width: 85%;
      input {
        background: transparent;
        border: 0px;
        -webkit-appearance: none;
        border-radius: 0px;
        padding: 12px 5px 12px 15px;
        color: $light_gray;
        height: 47px;
        caret-color: $cursor;
        &:-webkit-autofill {
          -webkit-box-shadow: 0 0 0px 1000px $bg inset !important;
          -webkit-text-fill-color: $cursor !important;
        }
      }
    }
    .el-form-item {
      border: 1px solid rgba(255, 255, 255, 0.1);
      background: rgba(0, 0, 0, 0.1);
      border-radius: 5px;
      color: #c0c0c0;
      .el-form-item__label{
          color: #c0c0c0;
      }
    }
    .el-button{
        width:100%;
    }
  }
</style>

<style rel="stylesheet/scss" lang="scss" scoped>
$bg:#2d3a4b;
$dark_gray:#889aa4;
$light_gray:#eee;

.login-container {
  min-height: 100%;
  width: 100%;
  background-color: $bg;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  .login-form {
    position: relative;
    width: 520px;
    max-width: 100%;
    padding: 160px 35px 0;
    margin: 0 auto;
    overflow: hidden;
  }
  .tips {
    font-size: 14px;
    color: #fff;
    margin-bottom: 10px;
    span {
      &:first-of-type {
        margin-right: 16px;
      }
    }
  }
  .svg-container {
    padding: 6px 5px 6px 15px;
    color: $dark_gray;
    vertical-align: middle;
    width: 30px;
    display: inline-block;
  }
  .title-container {
    position: relative;
    .title {
      font-size: 26px;
      color: $light_gray;
      margin: 0px auto 40px auto;
      text-align: center;
      font-weight: bold;
    }
    .set-language {
      color: #fff;
      position: absolute;
      top: 3px;
      font-size:18px;
      right: 0px;
      cursor: pointer;
    }
  }
  .show-pwd {
    position: absolute;
    right: 10px;
    top: 7px;
    font-size: 16px;
    color: $dark_gray;
    cursor: pointer;
    user-select: none;
  }
  .thirdparty-button {
    position: absolute;
    right: 0;
    bottom: 6px;
  }
}
</style>


