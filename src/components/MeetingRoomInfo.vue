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
      return [
        {
          location: 'room31',
          meetings: [[], [], [], [
            {
              id: 1,
              meeting: {
                topic: 'science',
                host: 'Yue',
                start: new Date(2020, 12, 16, 11, 10),
                end: new Date(2020, 12, 16, 16, 60),
                location: 'room31',
                attendee: [{ id: 1, user: 'yahzee' }, { id: 2, user: 'evo' }, { id: 3, user: 'uno' }],
              },
            },
          ], [], [
            {
              id: 1,
              meeting: {
                topic: 'math',
                host: 'Jeremy Lin',
                start: new Date(2020, 12, 18, 12, 30),
                end: new Date(2020, 12, 18, 14, 2),
                location: 'room31',
                attendee: [{ id: 1, user: 'george' }, { id: 2, user: 'roman' }, { id: 3, user: 'leonardo' }],
              },
            },
          ], [
            {
              id: 1,
              meeting: {
                topic: 'science',
                host: 'Daniel Lin',
                start: new Date(2020, 12, 19, 12, 19),
                end: new Date(2020, 12, 19, 16, 0),
                location: 'room31',
                attendee: [{ id: 1, user: 'daniel' }, { id: 2, user: 'mark' }, { id: 3, user: 'sam' }],
              },
            },
          ],
          ],
        },
        {
          location: 'room70',
          meetings: [[
            {
              id: 1,
              meeting: {
                topic: 'architecture',
                host: 'hyudai',
                start: new Date(2020, 12, 13, 5, 20),
                end: new Date(2020, 12, 13, 8, 30),
                location: 'room70',
                attendee: [{ id: 1, user: 'jolin' }, { id: 2, user: 'olivo' }, { id: 3, user: 'foxtrat' }],
              },
            },
          ], [], [
            {
              id: 1,
              meeting: {
                topic: 'physics',
                host: 'fandom',
                start: new Date(2020, 12, 15, 25, 6),
                end: new Date(2020, 12, 15, 27, 40),
                location: 'room70',
                attendee: [{ id: 1, user: 'rosvo' }, { id: 2, user: 'deli' }, { id: 3, user: 'alin' }],
              },
            },
            {
              id: 2,
              meeting: {
                topic: 'software',
                host: 'uganda',
                start: new Date(2020, 12, 15, 30, 70),
                end: new Date(2020, 12, 15, 40, 70),
                location: 'room70',
                attendee: [{ id: 1, user: 'quantun' }, { id: 2, user: 'fermi' }, { id: 3, user: 'einstein' }],
              },
            },
          ], [], [
            {
              id: 1,
              meeting: {
                topic: 'engineer',
                host: 'daniel',
                start: new Date(2020, 12, 17, 20, 40),
                end: new Date(2020, 12, 17, 22, 22),
                location: 'room70',
                attendee: [{ id: 1, user: 'quantun' }, { id: 2, user: 'fermi' }, { id: 3, user: 'einstein' }],
              },
            },
          ], [], [],
          ],
        },

      ];
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
