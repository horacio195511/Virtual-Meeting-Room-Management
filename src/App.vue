<template>
  <button v-on:click="home">Home</button>
    <component :is="present" @change-view="present = $event"></component>
</template>

<script>
import CancelMeeting from './components/CancelMeeting.vue';
import CreateMeeting from './components/CreateMeeting.vue';
import CreateReminder from './components/CreateReminder.vue';
import ForgetPassword from './components/ForgetPassword.vue';
import FullMeetingInfo from './components/FullMeetingInfo.vue';
import Login from './components/Login.vue';
import Main from './components/Main.vue';
import MeetingRoomInfo from './components/MeetingRoomInfo.vue';
import Signup from './components/Signup.vue';
import SimMeetInfo from './components/SimMeetInfo.vue';

export default {
  name: 'App',
  components: {
    CancelMeeting,
    CreateMeeting,
    CreateReminder,
    ForgetPassword,
    FullMeetingInfo,
    Login,
    Main,
    MeetingRoomInfo,
    Signup,
    SimMeetInfo,
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
