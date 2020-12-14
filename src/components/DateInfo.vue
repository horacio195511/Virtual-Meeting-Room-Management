<template>
    <td>
    <h4>{{ date }}</h4>
    <sim-meet-info v-for='meeting in meetings' :meeting='meeting' :key='meeting.id'
        :full-meeting-info="$emit('full-meeting-info', $event)"></sim-meet-info>
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
};
</script>
