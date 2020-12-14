<template>
    <!--button header-->
    <button>e mail</button>
    <button>create meeting</button>
    <button>meeting room information</button>
    <!--make it a component-->
    <calendar></calendar>
</template>

<script>
import Calendar from './Calendar'

export default {
    name: 'Main',
    components: {
        Calendar
    }
}
</script>

<style>

</style>