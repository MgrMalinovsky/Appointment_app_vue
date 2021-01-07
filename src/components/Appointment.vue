<template>
    <div class="container appointment">
        <div @click="toggleShow" class="title">
          {{ id+1 }}. {{ appointment.title }}
        </div>
        <div v-if="show" class="details">
          <p><strong>Fullname:</strong> {{ appointment.fullname }}</p>
          <p><strong>Mobile number:</strong> {{ appointment.number }}</p>
          <p><strong>Start of event:</strong> {{ printDate(appointment.start) }}</p>
          <p><strong>End of event:</strong> {{ printDate(appointment.end) }}</p>
          <p><strong>Location:</strong> {{ appointment.location }}</p>
          <p><strong>Notes:</strong> {{ appointment.notes }}</p>
          <button class="btn btn-primary" @click="editAppointment" style="margin-left: 5px;">
            Edit
          </button>
          <button class="btn btn-primary" @click="removeAppointment">
            Remove
          </button>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Appointment',
  props: ["appointment", "id", "editMethod", "removeMethod"],
  data() {
    return {
      show: false,
    }
  },
  methods: {
    printDate(date) {
      const split = date.split('T');
      return split[0].split('-').reverse().join('/') + ', ' + split[1];
    },
    toggleShow() {
      this.show = !this.show;
    },
    editAppointment() {
      this.editMethod(this.appointment);
    },
    removeAppointment() {
      const val = confirm("Why do you cum???");
      if (val) this.removeMethod(this.appointment);
    }
  }
}
</script>

<style scoped>
.appointment {
  background-color: #64b5f6;
  color: #FFFFFF;
  border-radius: 5px;
  margin-bottom: 2px;
  padding: 5px;
}

p {
  margin: 0;
}

.title {
  font-size: 24px;
}

.details {
  margin-top: 5px;
}

.details button {
  margin-top: 5px;
  margin-bottom: 5px;
}
</style>