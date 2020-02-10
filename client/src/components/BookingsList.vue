<template lang="html">
<div class="booking-item">
  <p>Customer List</p>

<div class="container">
  <div>Name </div>
  <div>Email</div>
  <div>Start</div>
  <div>End</div>
  <div class=""> Delete </div>
</div>

  <booking v-for="booking, index in bookings" :key="index"
  :booking="booking" />

</div>
</template>

<script>
import { eventBus } from '../main';
import BookingsServices from '../services/BookingsServices.js'
import Booking from './Booking.vue'

export default {
  name: 'bookings-list',
  data() {
    return {
      bookings: []
    }
  },
  'components': { Booking
  },
  mounted() {
    this.fetchData();
    eventBus.$on('booking-added', booking =>
  this.bookings.push(booking))

  eventBus.$on('booking-deleted', id => {
    const index = this.bookings.findIndex(booking => booking._id === id);
    this.bookings.splice(index, 1)
  })
},
methods: {
  fetchData(){
    BookingsServices.getBookings()
    .then(bookings => this.bookings = bookings);
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
