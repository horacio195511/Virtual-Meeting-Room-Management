<template>
    <table>
      <form>
        <tr>
          <td><label for="name">姓名</label></td>
          <td><input id="name" type="text" /></td>
        </tr>
        <tr>
          <td><label for="email">e-mail</label></td>
          <td><input id="email" type="email" /></td>
        </tr>
        <tr>
          <td><label for="account">帳號</label></td>
          <td><input id="account" type="text" /></td>
        </tr>
        <tr>
          <td><label for="password">密碼</label></td>
          <td><input id="password" type="password" /></td>
        </tr>
        <tr>
          <td><label for="password2">確認密碼</label></td>
          <td>
            <input
              id="password2"
              type="password"
              placeholder="再輸入一次密碼"
            />
          </td>
        </tr>
        <tr>
          <td><button type="button" v-on:click="signup">註冊</button></td>
        </tr>
      </form>
    </table>
</template>

<script>
export default {
    name: 'Signup'
}
</script>

<style>

</style>