<template>
    <div class="container">
      <h1>Appointment App</h1>
      <div class="row">
        <div class="col-4">
          <div class="alert alert-danger" v-if="alert.length != 0">
            <div v-for="item in alert" :key="item">
              {{ item }}
            </div>
          </div>
          <input-details :appointment.sync="appointment" />
          <div v-if="!editMode">
            <button class="btn btn-primary" @click="addAppointment">
              Add Appointment
            </button>
          </div>
          <div v-else>
            <button class="btn btn-primary" @click="saveChanges">
              Save changes
            </button>
            <button class="btn btn-primary" @click="cancelChanges">
              Cancer
            </button>
          </div>

        </div>
        
        <div class="col-8">
          <label for="sortby">Sort By</label>
          <select class="form-control" id="sortby" v-model="sortMode">
            <option value="title">Title</option>
            <option value="fullname">Fullname</option>
            <option value="time">Time</option>
          </select>
          <button @click="sortAppointments" class="btn btn-primary">
            Sort
          </button>

          <div v-for="(item, id) in appointments" :key="id">
            <appointment :appointment="item" :id="id" :editMethod=editAppointment :removeMethod="removeAppointment" />
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import Appointment from './Appointment.vue';
import InputDetails from './InputDetails.vue';

export default {
  name: 'AppointmentList',
  components: {
    Appointment,
    InputDetails
  },
  data() {
    let date = new Date().toISOString().substring(0, 16);
    return {
        appointment: {
          id: 0,
          title: "",
          fullname: "",
          number: "",
          start: date,
          end: date,
          location: "",
          notes: "",
        },
        appointments: [],
        editMode: false,
        id: -1,
        nextId: 0,
        alert: [],
        sortMode: "title",
    }
  },
  methods: {
    clearInput() {
      this.editMode = false;
      alert = [];
      this.appointment = {
        id: 0,
        title: "",
        fullname: "",
        number: "",
        start: new Date().toISOString().substring(0, 16),
        end: new Date().toISOString().substring(0, 16),
        location: "",
        notes: "",
      }
    },
    addAppointment() {
      this.alert = [];

      if (this.appointment.title.length < 3) {
        this.alert.push("Chuj 1");
      }

      if (this.appointment.fullname.length < 3) {
        this.alert.push("Chuj 2");
      }

      if (this.alert.length != 0) return;
      this.appointment.id = this.nextId++;
      this.appointments.push(this.appointment);
      this.clearInput();
    },
    editAppointment(item) {
      this.editMode = true;
      this.appointment = Object.assign({}, item);
    },
    saveChanges() {
      const id = this.appointments.find((item) => item.id == this.appointment.id).id;
      this.appointments[id] = this.appointment;
      this.clearInput();
    },
    cancelChanges() {
      this.editMode = true;
      this.clearInput();
    },
    removeAppointment(item) {
      this.appointments.splice(item, 1);
    },
    sortAppointments() {
      switch(this.sortMode) {
        case "title":
          this.appointments.sort((a, b) => a.title.localeCompare(b.title));
          break;
        case "fullname":
          this.appointments.sort((a, b) => a.fullname.localeCompare(b.fullname));
          break;
        case "time":
          this.appointments.sort((a, b) => a.start - b.start);
          break;
      }
    },
  }
}
</script>

<style scoped>
h1 {
  margin-top: 30px;
  margin-bottom: 50px;
  letter-spacing: 1px;
}

button {
  margin-top: 10px;
  margin-bottom: 10px;
}

label {
  font-size: 20px;
}
</style>