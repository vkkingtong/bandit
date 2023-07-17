<!--<template>-->
<!--  <div id="app">-->
<!--    <router-view />-->
<!--    <Login v-if="!isUserLoggedIn" @login-success="isUserLoggedIn = true" />-->
<!--  </div>-->
<!--</template>-->
<template>
  <div id="app">
    <template v-if="isUserLoggedIn">
      <router-view />
    </template>
    <template v-else>
      <Login @login-success="isUserLoggedIn = true" />
    </template>
  </div>
</template>
<script>

import Login from './Login.vue'
export default {
  name: 'App',
  components: {
    Login
  },
  data () {
    return {
      isUserLoggedIn: false// 根据实际登录状态判断是否显示登录组件
    }
  }
}
</script>>

<style>
* {
  margin: 0;
  padding: 0;
}
.clearfix {
  zoom: 1;
}
.clearfix:after {
  content: ".";
  display: block;
  visibility: hidden;
  height: 0;
  clear: both;
}
</style>
