<template>
  <div>
    <form>
        <table>
              <tr>
                  <td><label for="topic">主題</label></td>
                  <td><input id="topic" type="text"></td>
              </tr>
              <tr>
                  <td><label for="host">主持人</label></td>
                  <td><input id="host" type="text"></td>
              </tr>
              <tr>
                  <td><label for="start">開始</label></td>
                  <td><input id="start" type="datetime-local"></td>
              </tr>
              <tr>
                  <td><label for="end">結束</label></td>
                  <td><input id="end" type="datetime-local"></td>
              </tr>
              <tr>
                  <td><label for="location">地點</label></td>
                  <td><input id="location" type="text"></td>
              </tr>
              <tr>
                  <td><label for="remind">提醒</label></td>
                  <td><input id="remind" type="datetime-local"></td>
              </tr>
              <tr>
                  <td><input type="button" value="提交"></td>
              </tr>
        </table>
    </form>
  </div>
</template>

<script>
export default {
  name: 'CreateReminder',
  props: ['meeting'],
};
</script>

<style>

</style>
