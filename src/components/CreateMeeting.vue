<template>
  <div >
    <h2>Creat Meeting</h2>
      <form class="center">
            <table>
              <tr>
                  <td><label for="topic">主題</label></td>
                  <td><input id="topic" type="text" v-model="topic"></td>
              </tr>
              <tr>
                  <td><label for="host">主持人</label></td>
                  <td><input id="host" type="text" v-model="host"></td>
              </tr>
              <tr>
                  <td><label for="start">開始</label></td>
                  <td><input id="start" type="datetime-local" v-model="start"></td>
              </tr>
              <tr>
                  <td><label for="end">結束</label></td>
                  <td><input id="end" type="datetime-local" v-model="end"></td>
              </tr>
              <tr>
                  <td><label for="location">會議室</label></td>
                  <td><input id="location" type="text" v-model="location"></td>
              </tr>
              <tr>
                  <td><label for="attendee">參與人</label></td>
                  <td><input id="attendee" type="text" v-model="attendee"></td>
              </tr>
              <tr>
                  <td></td>
                  <td><button type="button" @click="create">{{ createText }}</button></td>
              </tr>
            </table>
      </form>
  </div>
</template>

<script>
export default {
  name: 'CreateMeeting',
  props: ['meeting'],
  methods: {
    create() {
      // call the api to store the meeting

      // if meeting create was successful, create reminder
      // data is bind to the form
      this.$emit('create-reminder');
    },
  },
  computed: {
    createText() {
      if (this.meeting === undefined) {
        return '建立';
      }
      return '編輯';
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
    attendee() {
      if (this.meeting !== undefined) {
        let tmp = '';
        this.meeting.attendee.forEach((element) => {
          tmp += `${element.user},`;
        });
        return tmp;
      }
      return '';
    },
  },
};
</script>

<style scoped>
.center{
  display: block;
  margin: auto;
  width: 30%;
}
td{
  width: 30%;
}
</style>
