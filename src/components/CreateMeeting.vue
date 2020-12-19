<template>
  <div >
    <h2>Creat Meeting</h2>
    <table class="center">
      <tr>
          <td class="labelright"><label for="topic">主題</label></td>
          <td class="inputleft"><input id="topic" type="text" v-model="topic"></td>
      </tr>
      <tr>
          <td class="labelright"><label for="host">主持人</label></td>
          <td class="inputleft"><input id="host" type="text" v-model="host"></td>
      </tr>
      <tr>
          <td class="labelright"><label for="start">開始</label></td>
          <td class="inputleft"><input id="start" type="datetime-local" v-model="start"></td>
      </tr>
      <tr>
          <td class="labelright"><label for="end">結束</label></td>
          <td class="inputleft"><input id="end" type="datetime-local" v-model="end"></td>
      </tr>
      <tr>
          <td class="labelright"><label for="location">會議室</label></td>
          <td class="inputleft"><input id="location" type="text" v-model="location"></td>
      </tr>
      <tr>
          <td class="labelright"><label>參與人</label></td>
          <td class="inputleft">
            <CancelUser
              v-for="attendee in attendees"
              :attendee="attendee"
              :key="attendee.id"
              @disinvite="disinvite">
            </CancelUser>
            <input type="text" v-model="newUser" @keydown="newAttendee($event)">
          </td>
      </tr>
      <tr>
          <td></td>
          <td><button type="button" @click="create">{{ createText }}</button></td>
      </tr>
    </table>
  </div>
</template>

<script>
import CancelUser from './CancelUser.vue';

export default {
  name: 'CreateMeeting',
  props: ['meeting'],
  components: {
    CancelUser,
  },
  data() {
    return {
      currentMeeting: this.meeting,
      newUser: '',
    };
  },
  methods: {
    create() {
      // call the api to store the meeting

      // if meeting create was successful, create reminder
      // data is bind to the form
      this.$emit('create-reminder');
    },
    disinvite(attendee) {
      // remove the user from the list of attendee in current meeting
      const index = this.currentMeeting.attendee.indexOf(attendee);
      this.currentMeeting.meeting.splice(index, 1);
      this.$forceUpdate();
      // send email to the user who are disinvite
    },
    newAttendee(event) {
      const keyCode = event.key;
      if (keyCode === 'Enter') {
        // Enter pressed
        // add the newUser to the list of attendee
        // push the last id+1 to the array
        const length = this.currentMeeting.attendee.length - 1;
        const newID = this.currentMeeting.attendee[length].id + 1;
        this.currentMeeting.attendee.push({ id: newID, user: this.newUser });
        this.newUser = '';
        this.$forceUpdate();
        // we somehow have to invite the new user, or just send email to all of them
      }
    },
  },
  computed: {
    createText() {
      if (this.meeting === undefined) {
        return '建立';
      }
      return '更新';
    },
    topic() {
      if (this.meeting !== undefined) {
        return this.meeting.topic;
      }
      return '';
    },
    host() {
      if (this.meeting !== undefined) {
        return this.meeting.host;
      }
      return '';
    },
    start() {
      if (this.meeting !== undefined) {
        return this.meeting.start;
      }
      return '';
    },
    end() {
      if (this.meeting !== undefined) {
        return this.meeting.end;
      }
      return '';
    },
    location() {
      if (this.meeting !== undefined) {
        return this.meeting.location;
      }
      return '';
    },
    attendees() {
      if (this.meeting !== undefined) {
        return this.meeting.attendee;
      }
      return '';
    },
  },
};
</script>

<style scoped>
</style>
