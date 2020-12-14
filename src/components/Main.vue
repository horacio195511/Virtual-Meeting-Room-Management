<template>
    <!--button header-->
    <button>e mail</button>
    <button @click="$emit('change-view', 'CreateMeeting')">create meeting</button>
    <button @click="$emit('change-view', 'MeetingRoomInfo')">meeting room information</button>
    <!--make it a component-->
    <calendar :initialdate="currentDate"></calendar>
</template>

<script>
import Calendar from './Calendar.vue';

export default {
  name: 'Main',
  data() {
    return {
      currentDate: new Date(),
    };
  },
  components: {
    Calendar,
  },
};
</script>

<style>

</style>
