<template>
  <div>
    <h1>Creat Meeting</h1>
    <table class="center">
      <tr>
          <td class="labelright"><label for="topic">主題</label></td>
          <td class="inputleft">
            <input id="topic" type="text" v-model="topic">
          </td>
      </tr>
      <tr>
          <td class="labelright"><label for="host">主持人</label></td>
          <td class="inputleft">
            <input id="host" type="text" v-model="host">
          </td>
      </tr>
      <tr>
          <td class="labelright"><label for="start">開始</label></td>
          <td class="inputleft">
            <input id="start" type="datetime-local" v-model="start">
          </td>
      </tr>
      <tr>
          <td class="labelright"><label for="end">結束</label></td>
          <td class="inputleft">
            <input id="end" type="datetime-local" v-model="end">
          </td>
      </tr>
      <tr>
          <td class="labelright"><label for="room">會議室</label></td>
          <td class="inputleft">
            <input id="room" type="text" v-model="room">
          </td>
      </tr>
      <tr>
          <td class="labelright"><label for="attendee">參與人</label></td>
          <td class="inputleft">
            <input id="attendee" type="text" v-model="attendee">
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
// import CancelUser from './CancelUser.vue';

export default {
  name: 'CreateMeeting',
  props: ['meeting'],
  // components: {
  //   CancelUser,
  // },
  data() {
    return {
      currentMeeting: this.meeting,
      newUser: '',
    };
  },
  methods: {
    create() {
      // call the api to store the meeting
      // collect data from the from
      // distinguish between edit and create
      let id;
      if (this.meeting === undefined) id = 0;
      else id = this.meeting.id;
      const formdata = new FormData();
      formdata.append('id', id);
      formdata.append('topic', this.topic);
      formdata.append('host', this.host);
      // time format need debug
      formdata.append('start', this.start);
      formdata.append('end', this.end);
      formdata.append('room', this.room);
      formdata.append('attendee', this.attendees);
      fetch('http://localhost:7000/test/v1/meeting_create', {
        method: 'POST',
        mode: 'cors',
        credentials: 'same-origin',
        body: formdata,
      }).then((response) => {
        if (!response.ok) {
          throw new Error('fetch error!!');
        } else {
          return response.json();
        }
      }).then((jsonResponse) => {
        if (jsonResponse.result === 0) {
          console.log('create success');
          this.$emit('create-reminder');
        } else console.log('create fail');
      }).catch((error) => {
        console.error(error);
      });
      // if meeting create was successful, create reminder
      // data is bind to the form
    },
    updateValue() {
      this.topic = this.meeting.topic;
      this.host = this.meeting.host;
      this.start = this.meeting.start;
      this.end = this.meeting.end;
      this.room = this.meeting.room;
      this.attendee = this.meeting.attendee;
    },
  },
  computed: {
    createText() {
      if (this.meeting !== undefined) {
        this.updateValue();
        return '建立';
      }
      return '更新';
    },
  },
};
</script>
