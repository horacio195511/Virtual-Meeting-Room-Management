<template>
  <td>
      <div v-for="user in usersArr" :key="user">
        <button @click="disinvite(user)">X</button><label>{{ user }}</label>
      </div>
      <input type="text" @keypress="onEnterPress" v-model="newUser">
  </td>
</template>

<script>
export default {
  name: 'CancelUser',
  props: ['attendees'],
  data() {
    return {
      usersObj: this.attendees,
      newUser: '',
    };
  },
  computed:{
    usersArr (){
      let tmp = [];
      this.usersObj.forEach(element => {
        tmp.push(element.user);
      });
    }
  },
  methods: {
    // there is something make the page reload !!
    disinvite(user) {
      this.usersArr.slice(this.users.indexOf(),1)
    },
    onEnterPress() {
      let e;
      if (!e) e = window.event;
      const keyCode = e.code || e.key;
      if (keyCode === 'Enter') {
        this.users.push({ id: this.users.length, user: this.newUser });
        this.newUser = '';
        // Enter pressed
        return true;
      }
      return false;
    },
  },
};
</script>

<style>

</style>
