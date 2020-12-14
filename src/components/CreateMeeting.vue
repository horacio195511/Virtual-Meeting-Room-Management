<template>
    <!--make it a component-->
    <table>
      <form>
        <tr>
          <td><label for="topic">主題</label></td>
          <td><input id="topic" type="text" /></td>
        </tr>
        <tr>
          <td><label for="host">主持人</label></td>
          <td><input id="host" type="text" /></td>
        </tr>
        <tr>
          <td><label for="start">開始時間</label></td>
          <td><input id="start" type="datetime" /></td>
        </tr>
        <tr>
          <td><label for="end">結束時間</label></td>
          <td><input id="end" type="datetime" /></td>
        </tr>
        <tr>
          <td><label for="attendee">參與人</label></td>
          <td><input id="attendee" type="text" /></td>
        </tr>
        <tr>
          <td><label for="meetingroom">會議室</label></td>
          <td><input id="meetingroom" type="text" /></td>
        </tr>
        <tr>
          <td><button type="button" @click="createMeeting">建立</button></td>
        </tr>
      </form>
    </table>
</template>

<script>
export default {
    name:'CreateMeeting',
    methods: {
                createMeeting: function(){
                    // get the data from form and send to server
                    alert('create meeting')
                },
    },
}
</script>

<style>

</style>