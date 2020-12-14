<template>
    <div>
        <h1>this is a calendar</h1>
        <table>
            <tr>
                <td>Sun</td><td>Mon</td><td>Tue</td><td>Wed</td><td>Thr</td><td>Fri</td><td>Sat</td>
            </tr>
            <tr><DateInfo v-for="date in cal[0]" :date='date.number' :key="date.id" :full-date-info="fullDateInfo"></DateInfo></tr>
            <tr><DateInfo v-for="date in cal[1]" :date='date.number' :key="date.id" :full-date-info="fullDateInfo"></DateInfo></tr>
            <tr><DateInfo v-for="date in cal[2]" :date='date.number' :key="date.id" :full-date-info="fullDateInfo"></DateInfo></tr>
            <tr><DateInfo v-for="date in cal[3]" :date='date.number' :key="date.id" :full-date-info="fullDateInfo"></DateInfo></tr>
            <tr><DateInfo v-for="date in cal[4]" :date='date.number' :key="date.id" :full-date-info="fullDateInfo"></DateInfo></tr>
        </table>
        <button @click="decMonth">last</button>
        <button>{{ currentYear }}/{{ currentMonth }}</button>
        <button @click="incMonth">next</button>
        <div :if="dateSelected">
            <full-meeting-info></full-meeting-info>
        </div>
    </div>
</template>

<script>
import DateInfo from './DateInfo'
import FullMeetingInfo from './FullMeetingInfo.vue'

export default {
    name: 'Calendar',
    props: ['initialdate'],
    components: {
        DateInfo,
        FullMeetingInfo,
    },
    methods:{
        fullDateInfo: function(){

        }
    },
    data: function(){
        return {
            currentDate: this.initialdate,
            currentMonth: this.initialdate.getMonth()+1,
            currentYear: this.initialdate.getFullYear(),
            cal: this.calGenerator(this.initialdate),
            //meeting request should be done here
            meetings: this.meetingRequest(),
            dateSelected: false
        }
    },
    methods: {
        meetingRequest: function () {
            return {name:"math", time:"0900"}
        },
        incMonth: function(){
            this.currentDate.setMonth(this.currentDate.getMonth()+1)
            this.currentMonth = this.currentDate.getMonth()+1
            this.currentYear = this.currentDate.getFullYear(),
            this.cal = this.calGenerator(this.currentDate)
        },
        decMonth: function(){
            this.currentDate.setMonth(this.currentDate.getMonth()-1)
            this.currentMonth = this.currentDate.getMonth()+1
            this.currentYear = this.currentDate.getFullYear(),
            this.cal = this.calGenerator(this.currentDate)
        },
        calGenerator: function(date){
            // render the calendar according to the month
            // in the form of
            // [
            //     [sun,mon,tue,wed,thr,fri,sat],
            //     [],
            //     [],
            //     [],
            //     []
            // ]
            // read the day of the first day
            // temporary parameter for passing the object reference mechanism of js...
            var initYear=date.getFullYear();
            var initMonth=date.getMonth();
            var initDate=date.getDate();
            var cal = [];
            // set the date to the first sunday
            date.setDate(1);
            date.setDate(date.getDate()-date.getDay());
            // fill the 7x5 array of cal
            for(i=0; i <=4; i++){
                cal.push([])
                for(j=0; j <= 6; j++){
                    cal[i].push({id:i ,number:date.getDate()});
                    date.setDate(date.getDate()+1);
                }
            }
            // recovery the original state
            date.setYear(initYear);
            date.setMonth(initMonth);
            date.setDate(initDate);
            return cal;
        }
    },
}
</script>