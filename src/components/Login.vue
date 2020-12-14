<template>
    <table>
      <form>
        <tr>
          <td><label for="account">帳號</label></td>
          <td><input id="account" type="text" /></td>
        </tr>
        <tr>
          <td><label for="password">密碼</label></td>
          <td><input id="password" type="password" /></td>
        </tr>
        <tr>
          <td><button type="button" v-on:click="signup">註冊</button></td>
          <td>
            <button type="button" v-on:click="forgetpassword">忘記密碼</button>
          </td>
          <td><button type="button" v-on:click="login">登入</button></td>
        </tr>
      </form>
    </table>
</template>

<script>
export default {
    name: 'Login'
}
</script>

<style>

</style>