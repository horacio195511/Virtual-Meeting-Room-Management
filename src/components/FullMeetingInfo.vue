<template>
  <div>
      <h2>Meeting Information</h2>
      <table class="center">
        <tr>
          <td>主題</td>
          <td>{{ meeting.topic }}</td>
        </tr>
        <tr>
          <td>主持人</td>
          <td>{{ meeting.host }}</td>
        </tr>
        <tr>
          <td>開始</td>
          <td>{{ meeting.start }}</td>
        </tr>
        <tr>
          <td>結束</td>
          <td>{{ meeting.end }}</td>
        </tr>
        <tr>
          <td>會議室</td>
          <td>{{ meeting.location }}</td>
        </tr>
        <tr>
          <td>參與人</td>
          <td><h5 v-for="attendee in meeting.attendee"
            :key="attendee.id">{{ attendee.user }} </h5></td>
        </tr>
        <tr>
          <td></td>
          <td><button @click="$emit('edit-meeting')">修改</button></td>
        </tr>
      </table>
  </div>
</template>

<script>
export default {
  name: 'FullMeetingInfo',
  props: ['meeting'],
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
