
<style lang="less" >
    @import "login.less";
</style>

<template>
   <div class="login">
       <vue-particles
        color="#F4F8F8"
        :particleOpacity="0.7"
        :particlesNumber="30"
        shapeType="star"
        :particleSize="4"
        linesColor="#ccc"
        :linesWidth="1"
        :lineLinked="true"
        :lineOpacity="0.4"
        :linesDistance="150"
        :moveSpeed="2"
        :hoverEffect="true"
        hoverMode="grab"
        :clickEffect="true"
        clickMode="push"
        class="vfx"
      >
      </vue-particles>

      <div class="container" >
      <div class="login-title">
        <p class="title-above test">Orange V-1.0</p>
        <p class="title-below test">欢迎使用橘子办公系统</p>
      </div>
    </div>

    <div class="login-con">
      <Card icon="log-in" title="欢迎登录" :bordered="false">
        <div class="form-con">
          <login-form @on-success-valid="handleSubmit"></login-form>
          <!-- <Form ref="loginForm" autocomplete="on" :model="loginForm" :rules="loginRules" class="card-box login-form">
                <Form-item prop="email">
                  <Input type="text" v-model="loginForm.email" placeholder="Username" autocomplete="on">
                       <Icon type="ios-person-outline" slot="prepend"></Icon>
                  </Input>
                </Form-item>
                <Form-item prop="password">
                    <Input type="text" v-model="loginForm.password" placeholder="Password" @keyup.enter.native="handleLogin">
                    <Icon type="ios-person-outline" slot="prepend"></Icon>
                    </Input>
                </Form-item>
                <FormItem>
                    <Button @click="handleLogin('loginForm')" type="primary" long>登录</Button>
                </FormItem>
            </Form> -->
          <p class="login-tip">输入用户名密码进行登录</p>
        </div>
      </Card>
    </div>
   </div>
</template>

<script>

import LoginForm from '../login/login-form'
import { mapActions } from 'vuex'
export default{
    components: {
        LoginForm
    },
    data(){
        return{
            
        }
    },
    methods: {
    ...mapActions([
      'handleLogin',
      'getUserInfo'
    ]),
    handleSubmit ({ userName, password }) {
      this.handleLogin({ userName, password }).then(res => {
        console.log(res)
        if (res.token === '') {
          console.log('暂无此账号')
          this.$Message.error('用户名或者密码输入错误')
        } else {
          this.getUserInfo().then(res => {
            this.$router.push({
              name: this.$config.homeName
            })
          })
        }
      })
    },
    handleLogin(){

    }
  }

}
</script>


