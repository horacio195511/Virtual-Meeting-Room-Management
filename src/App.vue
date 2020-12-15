<template>
  <button v-on:click="home">Home</button>
  <component :is="present" @change-view="present = $event"></component>
</template>

<script>
import ForgetPassword from './components/ForgetPassword.vue';
import Login from './components/Login.vue';
import Main from './components/Main.vue';
import MeetingRoomInfo from './components/MeetingRoomInfo.vue';
import CreateMeeting from './components/CreateMeeting.vue';
import Signup from './components/Signup.vue';

export default {
  name: 'App',
  components: {
    ForgetPassword,
    Login,
    Main,
    MeetingRoomInfo,
    CreateMeeting,
    Signup,
  },
  data() {
    return {
      present: 'Login',
      // for test, this parameter should set to false in production
      loggedIn: true,
    };
  },
  methods: {
    home() {
      if (this.loggedIn === false) {
        this.present = 'Login';
      } else {
        this.present = 'Main';
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
