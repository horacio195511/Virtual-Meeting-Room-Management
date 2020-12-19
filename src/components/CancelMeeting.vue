<template>
  <div>
      <h2>Cancel Meeting</h2>
      <table class="center">
        <tr>
          <td class="labelright">主題</td>
          <td class="inputleft">{{ meeting.topic }}</td>
        </tr>
        <tr>
          <td class="labelright">開始</td>
          <td class="inputleft">{{ meeting.start }}</td>
        </tr>
        <tr>
          <td class="labelright">結束</td>
          <td class="inputleft">{{ meeting.end }}</td>
        </tr>
        <tr>
          <td></td>
          <td class="inputleft"><button @click="cancelMeeting">發送</button></td>
        </tr>
      </table>
  </div>
</template>

<script>
export default {
  name: 'CancelMeeting',
  props: ['meeting'],
  methods: {
    cancelMeeting() {
      // call the api to cancel meeting
    },
  },
};
</script>

<style>
</style>
