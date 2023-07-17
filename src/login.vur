<template>
  <div class="login-container">
    <h2>登录</h2>
    <form @submit.prevent="login">
      <label for="username">用户名:</label>
      <input type="text" id="username" v-model="username" required>
      <label for="password">密码:</label>
      <input type="password" id="password" v-model="password" required>
      <button type="submit">登录</button>
    </form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      username: '',
      password: ''
    }
  },
  methods: {
    login () {
      if (this.username === 'root' && this.password === '123456') {
        // 登录成功
        this.$emit('login-success')
      } else {
        // 登录失败
        alert('用户名或密码错误')
      }
    }
  }
}
</script>

<style scoped>
.login-container {
  //width: 300px;
  //margin: 0 auto;
  //padding: 20px;
  //background-color: #f5f5f5;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-image: url('D:/JAVA/shengchan/coder/src/assets/images/image2.jpg'); /* 设置背景图像的路径 */
  background-size: cover;
  background-position: center;
  //border: 10px solid #ccc; /* 添加边框样式 */
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 10px;
}

input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 3px;
  box-sizing: border-box;
  margin-bottom: 15px;
}

button {
  width: 100%;
  padding: 10px;
  background-color: #409eff;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

button:hover {
  background-color: #1d8ce0;
}
</style>
