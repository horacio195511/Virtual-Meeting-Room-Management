<template>
  <button v-on:click="main">Home</button>
  <component :is="present"></component>
</template>

<script>
import Calendar from './components/Calendar.vue';
import CancelMeeting from './components/CancelMeeting';
import CreateMeeting from './components/CreateMeeting';
import CreateReminder from './components/CreateReminder';
import DateInfo from './components/DateInfo.vue';
import ForgetPassword from './components/ForgetPassword';
import FullMeetingInfo from './components/FullMeetingInfo';
import Login from './components/Login';
import Main from './components/Main';
import MeetingRoomInfo from './components/MeetingRoomInfo'
import Signup from './components/Signup'
import SimMeetInfo from './components/SimInfo.vue';


export default {
  name: 'App',
  components: {
    Calendar,
    CancelMeeting,
    CreateMeeting,
    CreateReminder,
    DateInfo,
    ForgetPassword,
    FullMeetingInfo,
    Login,
    Main,
    MeetingRoomInfo,
    Signup,
    SimMeetInfo,
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
