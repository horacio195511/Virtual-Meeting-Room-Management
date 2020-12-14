<template>
    <h6 @click="$emit('full-meeting-info')">{{ meeting.name }}於{{ meeting.time }}</h6>
</template>

<script>
export default {
    name: 'SimMeetInfo',
    props: ['meeting']
}
</script>