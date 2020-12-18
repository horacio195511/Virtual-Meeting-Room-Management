<template>
    <!--make it a component-->
    <div>
        <h2>Meeting Room Information</h2>
        <h3>{{ currentMonth }}</h3>
        <table>
          <!-- date number column-->
          <tr>
            <td>Sun</td>
            <td>Mon</td>
            <td>Tue</td>
            <td>Wed</td>
            <td>Thr</td>
            <td>Fri</td>
            <td>Sat</td>
          </tr>
          <tr>
            <td v-for="date in calWeek" :key="date.id">
              {{ date.date }}
            </td>
          </tr>
        </table>
        <button @click="decWeek">last</button>
        {{ currentMonth }}/{{ currentDay }}
        <button @click="incWeek">next</button>
    </div>
</template>

<script>
// import DateInfo from './DateInfo.vue';

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
    };
  },
  methods: {
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
        calWeek.push({ id: i, date: date.getDate() });
        date.setDate(date.getDate() + 1);
      }
      // reset the date
      date.setYear(initYear);
      date.setMonth(initMonth);
      date.setDate(initDate);
      console.log(calWeek);
      return calWeek;
    },
  },
  components: {
    // DateInfo,
  },
};
</script>

<style>

</style>
