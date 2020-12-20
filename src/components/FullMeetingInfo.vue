<template>
  <div>
      <h1>Meeting Information</h1>
      <table class="center">
        <tr>
          <td class="labelright">主題</td>
          <td class="inputleft">{{ meeting.topic }}</td>
        </tr>
        <tr>
          <td class="labelright">主持人</td>
          <td class="inputleft">{{ meeting.host }}</td>
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
          <td class="labelright">會議室</td>
          <td class="inputleft">{{ meeting.location }}</td>
        </tr>
        <tr>
          <td class="labelright">參與人</td>
          <td class="inputleft">
            <span
              v-for="attendee in meeting.attendee"
              :key="attendee.id"
            >{{ attendee.user }}, </span>
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
</style>
