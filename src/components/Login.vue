<template>
<div>
  <table class="center">
    <tr>
      <td><label for="account" class="labelright">帳號</label></td>
      <td><input id="account" type="text" class="inputleft" v-model="account"></td>
    </tr>
    <tr>
      <td><label for="password" class="labelright">密碼</label></td>
      <td><input id="password" type="password" class="inputleft" v-model="password"></td>
    </tr>
    <tr>
      <td><button @click="login">登入</button></td>
      <td><button @click="$emit('change-view','Signup')">註冊</button></td>
      <td><button @click="$emit('change-view','ForgetPassword')">忘記密碼</button></td>
    </tr>
  </table>
</div>
</template>

<script>
export default {
  name: 'Login',
  methods: {
    login() {
      //
    },
  },
};
</script>

<style scoped>
.center{
  display: block;
  margin: auto;
  width: 80%;
}
.labelright{
  text-align: right;
  width: 50%;
}
.inputleft{
  text-align: left;
  width: 50%;
}
</style>
