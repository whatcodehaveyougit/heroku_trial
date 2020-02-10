<template lang="html">

  <div class="container">

    <div>{{ booking.name }} </div>
    <div>{{ booking.email }}</div>
    <div>{{ booking.startDate }}</div>
    <div>{{ booking.endDate }}</div>
    <button type="button" v-on:click="deleteBooking(booking._id)" name="button">Delete</button>
  </div>

</template>

<script>
import { eventBus } from '../main'
import BookingsServices from '../services/BookingsServices';


export default {
  name: 'booking',
  props: ['booking'],
  methods: {
    deleteBooking(id) {
      BookingsServices.deleteBooking(id)
      .then(response => eventBus.$emit('booking-deleted', id));
    }
  }
}
</script>

<style lang="css" scoped>

.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
}
</style>
