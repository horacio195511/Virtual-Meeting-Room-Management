<template>
    <td>
    <h4>{{ date }}</h4>
    <sim-meet-info v-for='meeting in meetings' :meeting='meeting' :key='meeting.id' :full-meeting-info="$emit('full-meeting-info')"></sim-meet-info>
    </td>
</template>

<script>
import SimMeetInfo from './SimMeetInfo'
import SimMeetInfo from './SimMeetInfo.vue'

export default {
    name: 'DateInfo',
    props: ['date'],
    components: {
        SimMeetInfo
    },
    data: function(){
        return{
            meetings:[
                {id:1,name:'computer', time:'0920'},
            ]
        }
    }
}
</script>