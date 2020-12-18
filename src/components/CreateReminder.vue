<template>
  <div>
    <h2>Create Reminder</h2>
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
            <td class="labelright"><label for="attendee">參與人</label></td>
            <td class="inputleft"><input id="attendee" type="text" v-model="attendee"></td>
        </tr>
        <tr>
            <td class="labelright"><label for="remind">提醒</label></td>
            <td class="inputleft"><input id="remind" type="datetime-local"></td>
        </tr>
        <tr>
            <td></td>
            <td><button @click='create'>建立</button></td>
        </tr>
      </table>
  </div>
</template>

<script>
export default {
  name: 'CreateReminder',
  props: ['meeting'],
  methods: {
    create() {
      // sent request to API

      // go back to info
      this.$emit('full-meeting-info');
    },
  },
  computed: {
    topic() {
      if (this.meeting !== undefined) {
        return this.meeting.meeting.topic;
      }
      return '';
    },
    host() {
      if (this.meeting !== undefined) {
        return this.meeting.meeting.host;
      }
      return '';
    },
    start() {
      if (this.meeting !== undefined) {
        return this.meeting.meeting.start;
      }
      return '';
    },
    end() {
      if (this.meeting !== undefined) {
        return this.meeting.meeting.end;
      }
      return '';
    },
    location() {
      if (this.meeting !== undefined) {
        return this.meeting.meeting.location;
      }
      return '';
    },
    attendee() {
      if (this.meeting !== undefined) {
        let tmp = '';
        this.meeting.meeting.attendee.forEach((element) => {
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
}
.labelright{
  text-align: right;
  width: 50%;
}
.inputleft{
  text-align: left;
  width: 50%;
}
</style>
