<template>
    <h6
      @click="$emit('full-meeting-info', meeting)"
      class="meeting"
    >
      {{ shortInfo }}
    </h6>
</template>

<script>
export default {
  name: 'SimMeetInfo',
  props: ['meeting'],
  computed: {
    shortInfo() {
      let temp;
      if (this.meeting !== undefined) {
        const { topic } = this.meeting.meeting;
        const { date } = this.meeting.meeting;
        temp = `${topic}@${date.getHours()}:${date.getMinutes()}`;
      } else {
        temp = '';
      }
      return temp;
    },
  },
};
</script>

<style scoped>
.meeting{
  height:20%;
  border-bottom: 2px solid rgb(0, 38, 255);
  padding: 3px;
  margin: 3px;
}
</style>
