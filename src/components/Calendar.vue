<template>
    <div>
      <h1>Calendar</h1>
        <h3>{{ currentMonth }}</h3>
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
              :key="date.id">
            </DateInfo>
            </tr>
            <tr>
            <DateInfo
              v-for="date in cal[0]"
              :key="date.id"
              :meetings="meetings[date.number]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo></tr>

            <tr>
            <DateInfo
              v-for="date in cal[1]"
              :date='date.number'
              :key="date.id">
            </DateInfo>
            </tr>
            <tr>
            <DateInfo
              v-for="date in cal[1]"
              :key="date.id"
              :meetings="meetings[date.number]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo></tr>

            <tr>
            <DateInfo
              v-for="date in cal[2]"
              :date='date.number'
              :key="date.id">
            </DateInfo>
            </tr>
            <tr>
            <DateInfo
              v-for="date in cal[2]"
              :key="date.id"
              :meetings="meetings[date.number]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo></tr>

            <tr>
            <DateInfo
              v-for="date in cal[3]"
              :date='date.number'
              :key="date.id">
            </DateInfo>
            </tr>
            <tr>
            <DateInfo
              v-for="date in cal[3]"
              :key="date.id"
              :meetings="meetings[date.number]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo></tr>

            <tr>
            <DateInfo
              v-for="date in cal[4]"
              :date='date.number'
              :key="date.id">
            </DateInfo>
            </tr>
            <tr>
            <DateInfo
              v-for="date in cal[4]"
              :key="date.id"
              :meetings="meetings[date.number]"
              @full-meeting-info="$emit('full-meeting-info', $event)">
            </DateInfo></tr>
        </table>
          <button
            @click="decMonth"
            class="bottombutton"
          >
            <img
              src="../assets/last.png"
              class="buttonimage"
            >
          </button>
          {{ currentYear }}/{{ currentMonth }}
          <button
            @click="incMonth"
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
  name: 'Calendar',
  props: ['initialdate'],
  components: {
    DateInfo,
  },
  data() {
    return {
      currentDate: this.initialdate,
      currentMonth: this.initialdate.getMonth() + 1,
      currentYear: this.initialdate.getFullYear(),
      cal: this.calGenerator(this.initialdate),
      // meeting request should be done here
      meetings: this.meetingRequest(),
    };
  },
  methods: {
    // since different calendar needs different form of meeting,
    // so the meetingRequest put here
    meetingRequest() {
      // get meeting list of the specific month from server
      const rawMeetings = [
        {
          topic: 'science',
          host: 'Daniel Lin',
          start: new Date(2020, 12, 20, 15, 30),
          end: new Date(2020, 12, 20, 16, 0),
          location: 'room31',
          attendee: [{ id: 1, user: 'daniel' }, { id: 2, user: 'mark' }, { id: 3, user: 'sam' }],
        },
        {
          topic: 'math',
          host: 'Jeremy Lin',
          start: new Date(2020, 12, 18, 12, 30),
          end: new Date(2020, 12, 18, 14, 2),
          location: 'hall1',
          attendee: [{ id: 1, user: 'george' }, { id: 2, user: 'roman' }, { id: 3, user: 'leonardo' }],
        },
        {
          topic: 'science',
          host: 'Yue',
          start: new Date(2020, 12, 21, 11, 10),
          end: new Date(2020, 12, 21, 16, 60),
          location: 'room34',
          attendee: [{ id: 1, user: 'yahzee' }, { id: 2, user: 'evo' }, { id: 3, user: 'uno' }],
        },
        {
          topic: 'architecture',
          host: 'hyudai',
          start: new Date(2020, 12, 22, 5, 20),
          end: new Date(2020, 12, 22, 8, 30),
          location: 'room70',
          attendee: [{ id: 1, user: 'jolin' }, { id: 2, user: 'olivo' }, { id: 3, user: 'foxtrat' }],
        },
        {
          topic: 'physics',
          host: 'fandom',
          start: new Date(2020, 12, 15, 25, 6),
          end: new Date(2020, 12, 15, 27, 40),
          location: 'room31',
          attendee: [{ id: 1, user: 'rosvo' }, { id: 2, user: 'deli' }, { id: 3, user: 'alin' }],
        },
        {
          topic: 'engineer',
          host: 'daniel',
          start: new Date(2020, 12, 11, 20, 40),
          end: new Date(2020, 12, 11, 22, 22),
          location: 'hall1',
          attendee: [{ id: 1, user: 'quantun' }, { id: 2, user: 'fermi' }, { id: 3, user: 'einstein' }],
        },
        {
          topic: 'software',
          host: 'uganda',
          start: new Date(2020, 12, 15, 30, 70),
          end: new Date(2020, 12, 15, 40, 70),
          location: 'stub11',
          attendee: [{ id: 1, user: 'quantun' }, { id: 2, user: 'fermi' }, { id: 3, user: 'einstein' }],
        },
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
