<template>
    <!--button header-->
    <button>e mail</button>
    <button @click="createMeeting">create meeting</button>
    <button @click="changeLeftCol">{{ invertLeftCol }}</button>
    <!-- 2 column view-->
    <div class="row">
      <div class="column left">
        <!--left column-->
        <!--for calendar and meeting room information-->
        <component
          :is="leftcol"
          :initialdate="initialdate"
          @full-meeting-info="fullMeetingInfo">
        </component>
      </div>
      <div class="column right">
        <!--right column-->
        <component
          :is="rightcol"
          :meeting = "selectedMeeting"
          @full-meeting-info = "rightcol = 'FullMeetingInfo'"
          @edit-meeting = "rightcol = 'CreateMeeting'"
          @create-reminder = "rightcol = 'CreateReminder'"
          @cancel-meeting = "rightcol = 'CancelMeeting'"
          ></component>
      </div>
    </div>
</template>

<script>
import Calendar from './Calendar.vue';
import FullMeetingInfo from './FullMeetingInfo.vue';
import CreateMeeting from './CreateMeeting.vue';
import CreateReminder from './CreateReminder.vue';
import CancelMeeting from './CancelMeeting.vue';
import MeetingRoomInfo from './MeetingRoomInfo.vue';

export default {
  name: 'Main',
  props: ['initialdate'],
  data() {
    return {
      leftcol: 'Calendar',
      rightcol: '',
      // should be modified to the return meeting of calendar or meeting room
      // information component
      selectedMeeting: undefined,
    };
  },
  components: {
    Calendar,
    FullMeetingInfo,
    CreateMeeting,
    CreateReminder,
    CancelMeeting,
    MeetingRoomInfo,
  },
  computed: {
    invertLeftCol() {
      if (this.leftcol === 'Calendar') {
        return 'Meeting Room Information';
      }
      return 'Calendar';
    },
  },
  methods: {
    fullMeetingInfo(meeting) {
      this.selectedMeeting = meeting;
      this.rightcol = 'FullMeetingInfo';
    },
    createMeeting() {
      // provide an empty form
      this.selectedMeeting = undefined;
      this.rightcol = 'CreateMeeting';
    },
    changeLeftCol() {
      if (this.leftcol === 'Calendar') {
        this.leftcol = 'MeetingRoomInfo';
      } else {
        this.leftcol = 'Calendar';
      }
    },
  },
};
</script>

<style>
.row{
  display: flex;
  height: 100%;
}
.column{
  flex: 100%;
}
.left{
  flex: 70%;
}
.right{
  flex: 30%;
}
</style>
