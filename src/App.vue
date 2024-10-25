<template>
  <main class="mx-auto my-8 space-y-8">
    <h1 class="text-4xl font-medium">Event Booking app</h1>
    <h2 class="text-2xl font-medium">All events</h2>
    <section class="grid grid-cols-2 gap-8">
      <EventList></EventList>
    </section>
    <h2 class="text-2xl font-medium">Your Bookings</h2>
    <section class="grid grid-cols-1 gap-4">
      <template v-if="!bookingsLoading">
        <BookingItem
          v-for="booking in bookings"
          :key="booking.id"
          :event-title="booking.eventTitle"
          :status="booking.status"
          @cancel="cancelHandler(booking.id)"
        ></BookingItem>
      </template>
      <template v-else>
        <LoadingBookingsCard v-for="i in 4" :key="i"></LoadingBookingsCard
      ></template>
    </section>
  </main>
</template>
<script setup>
/*
console.log(
  'hmm so the beforecreate/Created hook has run the refs,computed and methods are available for parent(App)'
)
onMounted(() => {
  console.log('App(parent) mounted')
  })
  onBeforeMount(() => {
    console.log('BeforeMount hook of App(parent)')
    })
    */
import { onMounted } from 'vue'
import BookingItem from './components/BookingItem.vue'
import LoadingBookingsCard from './components/LoadingBookingsCard.vue'
import EventList from './components/EventList.vue'
import useBookings from './composables/useBookings'
const { bookings, bookingsLoading, fetchBookings, cancelHandler } = useBookings()

onMounted(() => {
  fetchBookings()
})
</script>
