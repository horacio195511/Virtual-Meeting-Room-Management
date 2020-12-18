<template>
  <div>
      <h2>Meeting Information</h2>
      <table class="center">
        <tr>
          <td class="labelright">主題</td>
          <td class="inputleft">{{ meeting.meeting.topic }}</td>
        </tr>
        <tr>
          <td class="labelright">主持人</td>
          <td class="inputleft">{{ meeting.meeting.host }}</td>
        </tr>
        <tr>
          <td class="labelright">開始</td>
          <td class="inputleft">{{ meeting.meeting.start }}</td>
        </tr>
        <tr>
          <td class="labelright">結束</td>
          <td class="inputleft">{{ meeting.meeting.end }}</td>
        </tr>
        <tr>
          <td class="labelright">會議室</td>
          <td class="inputleft">{{ meeting.meeting.location }}</td>
        </tr>
        <tr>
          <td class="labelright">參與人</td>
          <td class="inputleft">
            <div
              v-for="attendee in meeting.meeting.attendee"
              :key="attendee.id"
            >{{ attendee.user }}</div>
          </td>
        </tr>
        <tr>
          <td></td>
          <td>
            <button @click="$emit('edit-meeting')">編輯</button>
            <button @click="$emit('cancel-meeting')">取消會議</button>
          </td>
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
