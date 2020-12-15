<template>
<div>
  <table class="center">
    <tr>
      <td><label for="acccount">帳號</label></td>
      <td><input id="account" type="text"></td>
    </tr>
    <tr>
      <td><label for="password">密碼</label></td>
      <td><input id="password" type="password"></td>
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
  width: 30%;
}
td{
  width: 30%;
}
</style>
