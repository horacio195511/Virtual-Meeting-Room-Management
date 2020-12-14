<template>
    <div>
        <h1>this is a calendar</h1>
        <table>
            <tr>
                <td>Sun</td><td>Mon</td><td>Tue</td><td>Wed</td><td>Thr</td><td>Fri</td><td>Sat</td>
            </tr>
            <tr><DateInfo v-for="date in cal[0]" :date='date.number' :key="date.id"
            :meetings="meetings[date.number]" :full-meeting-info="fullMeetingInfo">
            </DateInfo></tr>
            <tr><DateInfo v-for="date in cal[1]" :date='date.number' :key="date.id"
            :meetings="meetings[date.number]" :full-meeting-info="fullMeetingInfo">
            </DateInfo></tr>
            <tr><DateInfo v-for="date in cal[2]" :date='date.number' :key="date.id"
            :meetings="meetings[date.number]" :full-meeting-info="fullMeetingInfo">
            </DateInfo></tr>
            <tr><DateInfo v-for="date in cal[3]" :date='date.number' :key="date.id"
            :meetings="meetings[date.number]" :full-meeting-info="fullMeetingInfo">
            </DateInfo></tr>
            <tr><DateInfo v-for="date in cal[4]" :date='date.number' :key="date.id"
            :meetings="meetings[date.number]" :full-meeting-info="fullMeetingInfo">
            </DateInfo></tr>
        </table>
        <button @click="decMonth">last</button>
        <button>{{ currentYear }}/{{ currentMonth }}</button>
        <button @click="incMonth">next</button>
        <div v-if="meetingSelected">
            <full-meeting-info></full-meeting-info>
        </div>
    </div>
</template>

<script>
import DateInfo from './DateInfo.vue';
import FullMeetingInfo from './FullMeetingInfo.vue';

export default {
  name: 'Calendar',
  props: ['initialdate'],
  components: {
    DateInfo,
    FullMeetingInfo,
  },
  data() {
    return {
      currentDate: this.initialdate,
      currentMonth: this.initialdate.getMonth(),
      currentYear: this.initialdate.getFullYear(),
      cal: this.calGenerator(this.initialdate),
      // meeting request should be done here
      meetings: this.meetingRequest(),
      meetingSelected: false,
      selectedMeeting: undefined,
    };
  },
  methods: {
    fullMeetingInfo(meeting) {
      this.meetingSelected = true;
      this.selectedMeeting = meeting;
    },
    meetingRequest() {
      // get meeting list of the specific month from server
      const rawMeetings = [
        { date: new Date(2020, 12, 18, 12, 30), topic: 'math' },
        { date: new Date(2020, 12, 21, 11, 10), topic: 'science' },
        { date: new Date(2020, 12, 22, 5, 20), topic: 'architecture' },
        { date: new Date(2020, 12, 15, 25, 6), topic: 'physics' },
        { date: new Date(2020, 12, 11, 20, 40), topic: 'engineer' },
        { date: new Date(2020, 12, 15, 30, 70), topic: 'software' },
      ];
      // sort it according to day
      // ex:
      // meetings:[
      // [{id:1, meeting}, {id:2, meeting}],
      // [{id:3, meeting}],
      // ]
      const meetingsForDate = [];
      for (let i = 0; i <= 31; i += 1) {
        // create 31 empty array for 31 days in a month
        meetingsForDate.push([]);
      }
      let i = 0;
      rawMeetings.forEach((element) => {
        meetingsForDate[element.date.getDate()].push({ id: i += 1, meeting: element });
      });
      return meetingsForDate;
    },
    incMonth() {
      this.currentDate.setMonth(this.currentDate.getMonth() + 1);
      this.currentMonth = this.currentDate.getMonth() + 1;
      this.currentYear = this.currentDate.getFullYear();
      this.cal = this.calGenerator(this.currentDate);
    },
    decMonth() {
      this.currentDate.setMonth(this.currentDate.getMonth() - 1);
      this.currentMonth = this.currentDate.getMonth() + 1;
      this.currentYear = this.currentDate.getFullYear();
      this.cal = this.calGenerator(this.currentDate);
    },
    calGenerator(date) {
      // render the calendar according to the month
      // in the form of
      // [
      //     [sun,mon,tue,wed,thr,fri,sat],
      //     [{id:0, number:2},{id:1, number:3}],
      //     [],
      //     [],
      //     [],
      //     []
      // ]
      // read the day of the first day
      // temporary parameter for passing the object reference mechanism of js...
      const initYear = date.getFullYear();
      const initMonth = date.getMonth();
      const initDate = date.getDate();
      const cal = [];
      // set the date to the first sunday
      date.setDate(1);
      date.setDate(date.getDate() - date.getDay());
      // fill the 7x5 array of cal
      for (let i = 0; i <= 4; i += 1) {
        cal.push([]);
        for (let j = 0; j <= 6; j += 1) {
          cal[i].push({ id: j, number: date.getDate() });
          date.setDate(date.getDate() + 1);
        }
      }
      // recovery the original state
      date.setYear(initYear);
      date.setMonth(initMonth);
      date.setDate(initDate);
      return cal;
    },
  },
};
</script>
