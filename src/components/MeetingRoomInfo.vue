<template>
    <!--make it a component-->
    <div>
        <h1>Meeting Room Information</h1>
        <h3>{{ currentMonth }}</h3>
        <table class="calendar">
          <!-- date number column-->
          <tr>
            <td></td>
            <td class="dateRow">Sun</td>
            <td class="dateRow">Mon</td>
            <td class="dateRow">Tue</td>
            <td class="dateRow">Wed</td>
            <td class="dateRow">Thr</td>
            <td class="dateRow">Fri</td>
            <td class="dateRow">Sat</td>
          </tr>
          <tr>
            <td></td>
            <DateInfo
              v-for="date in calWeek"
              :key="date.id"
              :date="date.number"
            >
            </DateInfo>
          </tr>
          <tr v-for="room in meetings" :key="room.location">
            <td>{{ room.location }}</td>
            <DateInfo
              :meetings="room.meetings[0]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo>
            <DateInfo
              :meetings="room.meetings[1]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo>
            <DateInfo
              :meetings="room.meetings[2]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo>
            <DateInfo
              :meetings="room.meetings[3]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo>
            <DateInfo
              :meetings="room.meetings[4]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo>
            <DateInfo
              :meetings="room.meetings[5]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo>
            <DateInfo
              :meetings="room.meetings[6]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo>
          </tr>
        </table>
        <button
        @click="decWeek"
        class="bottombutton"
        >
          <img
            src="../assets/last.png"
            class="buttonimage"
          >
        </button>
        {{ currentMonth }}/{{ currentDay }}
        <button
          @click="incWeek"
          class="bottombutton"
        >
          <img
            src="../assets/next.png"
            class="buttonimage"
          >
        </button>
    </div>
</template>

<script>
import DateInfo from './DateInfo.vue';

export default {
  name: 'MeetingRoomInfo.vue',
  props: ['initialdate'],
  data() {
    return {
      currentDate: this.initialdate,
      // since Vue.js don't detect the change of date Object, we have to do this manually
      currentMonth: this.initialdate.getMonth() + 1,
      currentDay: this.initialdate.getDate(),
      calWeek: this.weekGenerator(this.initialdate),
      meetings: this.meetingRequest(),
    };
  },
  methods: {
    meetingRequest() {
      // get meeting list of the specific month from server
      const formdata = new FormData();
      let meetings;
      formdata.append('date', this.currentDate);
      fetch('http://localhost:7000/test/v1/get_meeting_info_week', {
        method: 'POST',
        body: formdata,
        credentials: 'same-origin',
        mode: 'cors',
      }).then((response) => {
        if (!response.ok) {
          throw new Error('fetch error!!');
        } else {
          return response.json();
        }
      }).then((jsonResponse) => {
        meetings = jsonResponse;
      }).catch((error) => {
        console.error(error);
      });
      return meetings;
    },
    incWeek() {
      this.currentDate.setDate(this.currentDate.getDate() + 7);
      this.currentMonth = this.currentDate.getMonth() + 1;
      this.currentDay = this.currentDate.getDate();
      this.calWeek = this.weekGenerator(this.currentDate);
    },
    decWeek() {
      this.currentDate.setDate(this.currentDate.getDate() - 7);
      this.currentMonth = this.currentDate.getMonth() + 1;
      this.currentDay = this.currentDate.getDate();
      this.calWeek = this.weekGenerator(this.currentDate);
    },
    weekGenerator(date) {
      // return the array of all of the date in the week for the currentDate
      // in the form of [{id:0, date:1}, ..., {id:6, date:7}]
      // buffer the current date
      const initYear = date.getFullYear();
      const initMonth = date.getMonth();
      const initDate = date.getDate();
      // set the current date to the first day of the week
      date.setDate(date.getDate() - date.getDay());
      const calWeek = [];
      let i = 0;
      for (;i <= 6; i += 1) {
        calWeek.push({ id: i, number: date.getDate() });
        date.setDate(date.getDate() + 1);
      }
      // reset the date
      date.setYear(initYear);
      date.setMonth(initMonth);
      date.setDate(initDate);
      return calWeek;
    },
  },
  components: {
    DateInfo,
  },
};
</script>

<style>

</style>
