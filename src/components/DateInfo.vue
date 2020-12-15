<template>
    <td :class="style">
      <div v-if="date !== undefined" class="no-pad">{{ date }}</div>
      <div>
        <sim-meet-info
          v-for='meeting in meetings'
          :key='meeting.id'
          :meeting='meeting'
          @full-meeting-info="$emit('full-meeting-info', $event)">
        </sim-meet-info>
      </div>
    </td>
</template>

<script>
import SimMeetInfo from './SimMeetInfo.vue';

export default {
  name: 'DateInfo',
  props: ['date', 'meetings'],
  components: {
    SimMeetInfo,
  },
  computed: {
    style() {
      if (this.date !== undefined) return 'date';
      return 'meetings';
    },
  },
};
</script>

<style scoped>
  .date{
    height: 5%;
    border: 2px solid gray;
    padding: 3px;
    margin: 3px;
  }
  .meetings{
    height: 100%;
    border: 2px solid black;
    padding: 5px
  }
  .no-pad{
    padding: 0px;
  }
</style>
