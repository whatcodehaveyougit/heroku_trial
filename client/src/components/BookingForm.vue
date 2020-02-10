<template>
  <div>
    <form class="" action="index.html" v-on:submit="createBooking" method="post">

      <label for="name" >Name</label>
      <input class="input" type="text" v-model="name" name="name" >

      <label for="email" >Email</label>
      <input class="input" type="text" name="name" v-model="email" >

      <label for="">Arrival Date</label>
      <input class="input" v-model="startDate" type="date" >

      <label for="">Departure Date</label>
      <input class="input" v-model="endDate" type="date">

      <input class="input" type="submit" value="Create Booking">

    </form>
  </div>
</template>

<script>
import BookingsServices from '../services/BookingsServices.js'
import { eventBus } from '../main'

export default {
  name: "customer-form",
  data() {
    return {
      name: "",
      email: "",
      startDate: null,
      endDate: null
    }
  },
  methods: {
    createBooking(evt) {
      evt.preventDefault(); // Stopping the refresh happen by default
      const payload  = {
        name: this.name,
        email: this.email,
        startDate: this.startDate,
        endDate: this.endDate
      };
      BookingsServices.postBooking(payload)
      .then( res => { eventBus.$emit('booking-added', res);
    })
  }
}

}

</script>

<style scoped>

.input{
  margin-right:20px;
}

</style>
