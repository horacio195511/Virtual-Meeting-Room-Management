<template>
  <table>
    <tr>
      <td><label for="email">email</label></td>
      <td><input type="email" placeholder="ex:xxx@mail.com" /></td>
    </tr>
    <tr>
      <!--not complete yet-->
      <td><button @click="sendPassword"></button></td>
    </tr>
  </table>
</template>

<script>
export default {
  name: 'ForgetPassword',
  methods: {
    sendPassword() {

    },
  },
};
</script>

<style>

</style>
