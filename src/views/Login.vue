<template>
    <div class="login">
        <div class="loginTable">
            <p class="left"></p>
            <p class="right"></p>
            <h2>经销商后台管理系统</h2>
            <el-form class="form" :model='loginForm' :rules='rules'>
                <el-form-item prop="user">
                    <label for="user"><span class="iconfont">&#xe63d;</span><el-input type="text" v-model="loginForm.user" id="user" placeholder="请输入账号"></el-input></label>
                </el-form-item>
                <el-form-item prop="password">
                    <label for="password"><span class="iconfont">&#xe62f;</span><el-input type="password" v-model="loginForm.password" id="password" placeholder="请输入账号"></el-input></label>
                </el-form-item>
                <el-button @click="login">登录</el-button>
                <p>忘记密码请联系管理员</p>
            </el-form>
        </div>
    </div>
</template>

<script>
import Qs from 'qs'
import axios from 'axios'
import store from '@/store';
export default {
    name:'Login',
    data(){
        return{
            loginForm:{
                user:'',
                password:''
            },
            rules:{
                user:[
                    {required: true, message: '请输入登录用户名',trigger: 'blur'},
                    //{ validator: validaePass }
                ],
                password: [
                    {required: true,message: '请输入登录密码', trigger: 'blur'},
                    //{ validator: validaePass2 }
                ],
            }
        }
    },
    methods:{
        login(){
            //登录
            var data={
                'user':this.loginForm.user,
                'password':this.loginForm.password
            }
            if(this.loginForm.user==''||this.loginForm.password==''){
                this.$alert('账号和密码不能为空!', '提示', {
                    confirmButtonText: '确定',
                });
            }else{
                store.dispatch('userLogin', data.user);
                this.$message({message:'欢迎'+this.$store.state.token+'!',type:'success'})
                this.$router.push('/')
            }
           
        }
    }
}
</script>

<style lang="scss" scoped>
    .login{
        width: 100%;
        height: 100%;
        background-image: url(../assets/images/login.png);
        background-size: 100% 100%;
        background-repeat: no-repeat;
    }
    .loginTable{
        width: 600px;
        height: 300px;
        // background: white;
        position: absolute;
        left: 50%;
        top:50%;
        text-align: center;
        margin-top: -150px;
        margin-left: -300px;
        border: 1px solid white;
        border-top: none;
        .form{
            padding-top: 40px;
            p{
                color: white;
                margin-top: 20px;
            }
        }
        .left{
            width: 170px;
            background: white;
            height: 1px;
            float: left;
        }
        label{
            display: flex;
            flex-direction: row;    
            align-items: center;
            color: white;
            border-bottom: 1px solid white;
            width: 300px;
            text-align: center;
            margin: 10px auto;
            justify-content: center;
            span{
                font-size: 28px;

            }
            
        }
        .el-input__inner{
            background: transparent;
            
        }
        .el-input{
            width: 180px;
            
            margin-left: 10px;
        }
        .right{
            width: 170px;
            background: white;
            height: 1px;
            float: right;
        }
        h2{
            color: white;
            position: absolute;
            left: 50%;
            font-weight: normal;
            font-size: 24px;
            transform: translateX(-50%);
            top:-20px;
            background: transparent;
            padding: 0 20px;
        }
    }
</style>

