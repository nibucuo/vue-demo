<template>
  <div class="top">
    <!-- 顶部欢迎菜单包括登录按钮，中英文切换 -->
    <div class="topMenu">
      <span class="welcome">您好，欢迎来到绿石诉讼资助！</span>
      <span class="login" v-show="!username" @click="showLogin">登录</span>
      <router-link tag="span" to="/Contact/InforList" class="login" v-show="username" >{{username}}</router-link>
      <span class="language"><!-- <span>English</span>/ --><span class="active">中文</span></span>
    </div>
    <div v-show="loginFlag" class="loginBg">
      <div class="loginBox">
        <div class="loginText">用户登录</div>
        <div class="loginTel">
          <span>手机号</span><input type="text" v-model="userTel" name="" placeholder="请输入您的手机号">
        </div>
        <div class="loginPwd">
          <span>密码</span><input type="password" v-model="userPwd" name="" placeholder="请输入您的密码">
        </div>
        <div class="loginBtn" @click="login">
          登录
        </div>
        <div class="closeLogin" @click="closeLogin">
          <img src="../../assets/images/closeLogin.png">
        </div>
      </div>
    </div>
    <!-- 顶部导航栏，左图右导航结构 -->
    <div v-bind:class="bgColor ==='white'?'topNavBoxWhite':'topNavBox'">
      <router-link to="/" tag="div" class="topNavLeft">
        <img v-if="bgColor == 'white'" src="../../assets/images/logo.png"/>
        <img v-else src="../../assets/images/logoBlank.png"/>
      </router-link>
      <!-- 此处有两个隐藏菜单（团队和博客），内容待定，同样还有TopNav.vue文件需要修改 -->
      <ul class="topNav">
        <router-link to="/" tag="li" exact >首页</router-link>
        <router-link to="/AboutUs" tag="li" exact >关于我们</router-link>
        <router-link to="/Funding" tag="li" exact >诉讼资助</router-link>
        <router-link to="/Team" style="display:none" tag="li" >团队/顾问</router-link>
        <router-link to="/Coverage" tag="li" exact >专业网络</router-link>
        <router-link to="/Blog" style="display:none" tag="li" >绿石研究院</router-link>
        <router-link to="/Scenarios" tag="li" exact >应用场景</router-link>
        <router-link to="/Contact" tag="li" >联系我们</router-link>
      </ul>
    </div>  
  </div>
  
</template>

<script>
import store from '@/vuex/store';
import {mapState,mapMutations} from 'vuex';

export default {
  name: 'TopNavBlack',
  store,
  data () {
    return {
    }
  },
  props: ['bgColor'],
  computed: {
    ...mapState(['loginFlag','userTel','userPwd','username','ownUri']),
    userTel : {
      get () {
        return this.$store.state.userTel
      },
      set (value) {
        this.$store.commit('updateUserTel', value)
      }
    },
    userPwd : {
      get () {
        return this.$store.state.userPwd
      },
      set (value) {
        this.$store.commit('updateUserPwd', value)
      }
    },
  },
  methods: {
    ...mapMutations(['showLogin','closeLogin','login']),
    init:function(){
      // console.log(this.bgColor);
    }
  },
  mounted: function(){
    this.init();
  },
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当钩子执行前，组件实例还没被创建
    console.log(to);
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
    console.log(from);
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
    console.log(next);
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/*顶部欢迎菜单包括登录按钮，中英文切换*/
.topMenu{
  width: 100%;
  height: 26px;
  background: #f0f0f0;
  position: fixed;
  left: 0;
  top: 0;
  z-index: 10;
}
.topMenu span{
  height: 26px;
  display: inline-block;
  line-height: 26px;
}
.welcome{
  margin-left: 5%;
  font-family: 'Bold';
  font-size: 12px;
  color: #333;
}
.login{
  margin-left: 2.5%;
  font-family: 'Normal';
  font-size: 12px;
  color: #c49a6d;
  cursor: pointer;
}
.language{
  margin-left: 63%;
  font-family: 'Normal';
  font-size: 12px;
  color: #333;
}
.language span{
  margin: 0 10px;
  /*cursor: pointer;*/
}
.language .active{
  color: #c49a6d;
}

/*登陆框*/
.loginBg{
  width: 100%;
  height: 100%;
  position: fixed;
  left: 0;
  bottom: 0;
  background: transparent;
  z-index: 11;
}
.loginBox{
  width: 285px;
  height: 240px;
  background: rgba(240,240,240,0.9);
  position: absolute;
  left: 50%;
  margin-left: -142.5px;
  top: 50%;
  margin-top: -130px;
  padding: 25px;
  box-sizing: border-box;
  border-radius: 10px;
  box-shadow: 0 0 14px 7px #ddd;
}
.loginBox div{
  width: 225px;
  height: 32px;
  margin-bottom: 20px;
  line-height: 32px;
  text-align: center;
}
.loginText{
  font-family: 'Regular';
  font-size: 21px;
  color: #333;
}
.loginTel{
  width: 100%;
  height: 32px;
  background: #fff;
  font-family: 'Normal';
  font-size: 15px;
  color: #4d4d4d;
}
.loginTel span{
  display: inline-block;
  width: 25%;
}
.loginPwd{
  width: 100%;
  height: 32px;
  background: #fff;
  font-family: 'Normal';
  font-size: 14px;
  color: #979797;
}
.loginPwd span{
  display: inline-block;
  width: 25%;
}
.loginTel input{
  width: 70%;
  height: 30px;
  line-height: 30px;
  border: none;
  background: #fff;
  font-family: 'Normal';
  font-size: 14px;
  color: #4d4d4d;
}
.loginPwd input{
  width: 70%;
  height: 28px;
  line-height: 28px;
  border: none;
  background: #fff;
  font-family: 'Normal';
  font-size: 13px;
  color: #979797;
}
.loginBtn{
  width: 100%;
  height: 38px;
  line-height: 38px;
  background: #c49a6d;
  border-radius: 5px;
  color: #fff;
  font-family: 'Normal';
  font-size: 14px;
  cursor: pointer;
}
.loginBox div.closeLogin{
  width: 16px;
  height: 16px;
  position: absolute;
  right: 20px;
  top: 20px;
}
.loginBox div.closeLogin img{
  width: 100%;
  cursor: pointer;
}
/*顶部导航栏，左图右导航结构*/
.topNavBoxWhite{
  width: 100%;
  height: 89px;
  background: #fff;
  position: fixed;
  top: 26px;
  left: 0;
  z-index: 10;
}
.topNavBox{
  width: 100%;
  height: 89px;
  background: rgba(0,0,0,0.7);
  position: fixed;
  top: 26px;
  left: 0;
  z-index: 10;
}
.topNavLeft{
  width: 20%;
  height: 85px;
  float: left;
  margin-left: 8%;
  margin-right: 4%;
  cursor: pointer;
}
.topNavLeft img{
  height: 51px;
  display: block;
  margin-top: 17px; 
}
.topNav{
  width: 66%;
  float: left;
  padding-top: 20px;
  line-height: 65px;
}
.topNav li{
  float: left;
  width: 9%;
  margin: 0 1%;
  font-family: 'Normal';
  font-size: 14px;
  border-bottom: 2px solid transparent;
  text-align: center;
  cursor: pointer;
  color: #fff;
}
.topNavBoxWhite li{
  color: #333;
}
.topNav li.active{
  color: #c49a6d;
  border-bottom: 4px solid #c49a6d;
}
</style>