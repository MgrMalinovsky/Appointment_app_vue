<template>
    <div class="container">
        <appointment-list/>
    </div>
</template>

<script>
import AppointmentList from './AppointmentList.vue';

export default {
  name: 'Main',
  components: {
    AppointmentList,
  }
}
</script>