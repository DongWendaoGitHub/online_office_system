<!---->
<template>
    <div>
        <!--el-form   表单-->
        <el-form :rules="rules" ref="loginForm" :model="loginForm" class="loginContainer">
            <h3 class="loginTitle">系统登录</h3>
            <el-form-item prop="username">
                <!--输入框-->
                <el-input type="text" auto-complete="false" v-model="loginForm.username" placeholder="请输入用户名"></el-input>
            </el-form-item>

            <el-form-item prop="password">
                <el-input type="password" auto-complete="false" v-model="loginForm.password" placeholder="请输入密码"></el-input>
            </el-form-item>

            <el-form-item prop="code">
                <el-input type="text" auto-complete="false" v-model="loginForm.code" placeholder="点击图片更换验证码" class="loginCode"></el-input>
                <img :src="captchaUrl">
            </el-form-item>

            <el-form-item>
                <el-checkbox v-model="checked" class="loginRemember">记住密码</el-checkbox>
                <el-button type="primary" class="loginButton" @click="submitLogin">登陆</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>

<script>
    export default {
        name: "Login",
        data(){
            return{
                captchaUrl:'',          /*验证码*/
                loginForm:{
                    username:'',
                    password:'lsp',
                    code:''              /*验证码*/
                },
                checked:true,

                rules:{
                    username:[{required:true,message:'用户名不能为空', trigger:'blur'}],
                    password:[{required:true,message:'密码不能为空', trigger:'blur'}],
                    code:[{required:true,message:'验证码不能为空', trigger:'blur'}]
                }

            }
        }
        ,
        methods:{
            submitLogin(){
                this.$refs.loginForm.validate((valid) => {
                    if (valid) {
                        this.$message({
                            message: '恭喜你，提交成功',
                            type: 'success'
                        });
                    } else {
                        console.log('error submit!!');
                        this.$message.error('错了哦，请输入完整信息');
                        return false;
                    }
                });
            }
        }
    }
</script>

<style>
    .loginContainer{
        border-radius: 15px;
        background-clip: padding-box;     /*背景*/
        margin: 188px auto;               /*边距*/
        width: 350px;
        padding: 15px 35px 15px 35px;     /*边距*/
        background: #fff;                 /*背景颜色*/
        border: 1px solid #eaeaea;        /*边框*/
        box-shadow: 0 0 25px #cac6c6;     /*阴影*/
    }

    .loginTitle{
        margin: 8px auto;/*内边距*/
        text-align: center;/*居中*/
    }

    .loginButton{
        margin-left: 200px;
    }

    .loginCode{
        margin-right: 5px;
        width: 180px;
    }

</style>