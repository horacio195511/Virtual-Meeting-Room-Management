<template>
<div>
  <table class="center">
    <tr>
      <td><label for="email">email</label></td>
      <td><input type="email" placeholder="ex:xxx@mail.com" /></td>
    </tr>
    <tr>
      <!--not complete yet-->
      <td></td>
      <td><button @click="sendPassword">送出</button></td>
    </tr>
  </table>
</div>
</template>

<script>
export default {
  name: 'ForgetPassword',
  methods: {
    sendPassword() {
      const formdata = new FormData();
      formdata.append('email', this.email);
      fetch('http://localhost:7000/test/v1/send_password', {
        method: 'POST',
        mode: 'cors',
        body: formdata,
        credentials: 'same-origin',
      });
    },
  },
};
</script>

<style>

</style>
