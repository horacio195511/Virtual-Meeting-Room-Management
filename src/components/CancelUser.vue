<template>
  <div>
    <button @click="$emit('disinvite', attendee)">X</button><label>{{ attendee.user }}</label>
  </div>
</template>

<script>
export default {
  name: 'CancelUser',
  props: ['attendee'],
  methods: {
    // there is something make the page reload !!
    onEnterPress() {
      let e;
      if (!e) e = window.event;
      const keyCode = e.code || e.key;
      if (keyCode === 'Enter') {
        this.users.push({ id: this.users.length, user: this.newUser });
        this.newUser = '';
        // Enter pressed
        return true;
      }
      return false;
    },
  },
};
</script>

<style>

</style>
