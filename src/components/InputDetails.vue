<template>
  <div>
    <form>
      <div class="form-group">
        <label for="title">Title</label>
        <input class="form-control" id="title" v-model="appointment.title">
      </div>
      <div class="form-group">
        <label for="fullname">Fullname</label>
        <input class="form-control" id="fullname" v-model="appointment.fullname">
      </div>
      <div class="form-group">
        <label for="number">Mobile number</label>
        <input class="form-control" id="number" v-model="appointment.number">
      </div>
      <div class="form-group">
        <label for="start">Start of event</label>
        <input type="datetime-local" class="form-control" id="start" v-model="appointment.start">
      </div>
      <div class="form-group">
        <label for="end">End of event</label>
        <input type="datetime-local" class="form-control" id="end" v-model="appointment.end">
      </div>
      <div class="form-group">
        <label for="location">Location</label>
        <input class="form-control" id="location" v-model="appointment.location">
      </div>
      <div class="form-group">
        <label for="notes">Notes</label>
        <input class="form-control" id="notes" v-model="appointment.notes">
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'InputDetails',
  props: ["appointment"],
}
</script>

<style scoped>
label {
  font-size: 20px;
}
</style>