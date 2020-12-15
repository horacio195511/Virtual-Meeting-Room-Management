<template>
    <div>
        <h1>{{ currentMonth }}</h1>
        <table class='calendar'>
            <tr>
                <td class="dateRow">Sun</td>
                <td class="dateRow">Mon</td>
                <td class="dateRow">Tue</td>
                <td class="dateRow">Wed</td>
                <td class="dateRow">Thr</td>
                <td class="dateRow">Fri</td>
                <td class="dateRow">Sat</td>
            </tr>
            <tr>
            <DateInfo
              v-for="date in cal[0]"
              :date='date.number'
              :key="date.id"
              @full-meeting-info="below='FullMeetingInfo'">
            </DateInfo>
            </tr>
            <tr>
            <DateInfo
              v-for="date in cal[0]"
              :key="date.id"
              :meetings="meetings[date.number]"
              @full-meeting-info="below='FullMeetingInfo'">
            </DateInfo>
            </tr>

            <tr>
            <DateInfo
              v-for="date in cal[1]"
              :date='date.number'
              :key="date.id"
              @full-meeting-info="below='FullMeetingInfo'">
            </DateInfo>
            </tr>
            <tr>
            <DateInfo
              v-for="date in cal[1]"
              :key="date.id"
              :meetings="meetings[date.number]"
              @full-meeting-info="below='FullMeetingInfo'">
            </DateInfo></tr>

            <tr>
            <DateInfo
              v-for="date in cal[2]"
              :date='date.number'
              :key="date.id"
              @full-meeting-info="below='FullMeetingInfo'">
            </DateInfo>
            </tr>
            <tr>
            <DateInfo
              v-for="date in cal[2]"
              :key="date.id"
              :meetings="meetings[date.number]"
              @full-meeting-info="below='FullMeetingInfo'">
            </DateInfo></tr>

            <tr>
            <DateInfo
              v-for="date in cal[3]"
              :date='date.number'
              :key="date.id"
              @full-meeting-info="below='FullMeetingInfo'">
            </DateInfo>
            </tr>
            <tr>
            <DateInfo
              v-for="date in cal[3]"
              :key="date.id"
              :meetings="meetings[date.number]"
              @full-meeting-info="below='FullMeetingInfo'">
            </DateInfo></tr>

            <tr>
            <DateInfo
              v-for="date in cal[4]"
              :date='date.number'
              :key="date.id"
              @full-meeting-info="below='FullMeetingInfo'">
            </DateInfo>
            </tr>
            <tr>
            <DateInfo
              v-for="date in cal[4]"
              :key="date.id"
              :meetings="meetings[date.number]"
              @full-meeting-info="below='FullMeetingInfo'">
            </DateInfo></tr>
        </table>
        <button @click="decMonth">last</button>
        <button>{{ currentYear }}/{{ currentMonth }}</button>
        <button @click="incMonth">next</button>
        <component
          class="component"
          :is="below"
          @full-meeting-info = "below = 'FullMeetingInfo'"
          @edit-meeting = "below = 'CreateMeeting'"
          @create-reminder = "below = 'CreateReminder'"
          :meeting = "fullMeetingData"></component>
    </div>
</template>

<script>
import CreateMeeting from './CreateMeeting.vue';
import CreateReminder from './CreateReminder.vue';
import DateInfo from './DateInfo.vue';
import FullMeetingInfo from './FullMeetingInfo.vue';

export default {
  name: 'Calendar',
  props: ['initialdate'],
  components: {
    CreateMeeting,
    CreateReminder,
    DateInfo,
    FullMeetingInfo,
  },
  data() {
    return {
      currentDate: this.initialdate,
      currentMonth: this.initialdate.getMonth() + 1,
      currentYear: this.initialdate.getFullYear(),
      cal: this.calGenerator(this.initialdate),
      // meeting request should be done here
      meetings: this.meetingRequest(),
      selectedMeeting: undefined,
      below: '',
    };
  },
  computed: {
    fullMeetingData() {
      // request from server
      return {
        topic: 'science',
        host: 'Daniel Lin',
        start: new Date(2020, 12, 20, 15, 30),
        end: new Date(2020, 12, 20, 16, 0),
        location: 'room31',
        attendee: [{ id: 1, user: 'daniel' }, { id: 2, user: 'mark' }, { id: 3, user: 'sam' }],
      };
    },
  },
  methods: {
    meetingRequest() {
      // get meeting list of the specific month from server
      const rawMeetings = [
        { start: new Date(2020, 12, 18, 12, 30), topic: 'math' },
        { start: new Date(2020, 12, 21, 11, 10), topic: 'science' },
        { start: new Date(2020, 12, 22, 5, 20), topic: 'architecture' },
        { start: new Date(2020, 12, 15, 25, 6), topic: 'physics' },
        { start: new Date(2020, 12, 11, 20, 40), topic: 'engineer' },
        { start: new Date(2020, 12, 15, 30, 70), topic: 'software' },
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
        meetingsForDate[element.start.getDate()].push({ id: i += 1, meeting: element });
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

<style scoped>
.calendar{
  border: 2px solid rgb(0, 0, 0);
  border-radius: 10px;
  width: 80%;
  height: 50%;
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.dateRow{
  width: 5%;
  overflow: hidden;
  border-bottom: 2px solid black;
  border-right: 2px solid black;
  border-left: 2px solid black;
}
.component{
  display: block;
  margin-left: auto;
  margin-right: auto;
}
</style>
