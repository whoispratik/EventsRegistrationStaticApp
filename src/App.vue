<template>
  <main class="mx-auto my-8 space-y-8">
    <h1 class="text-4xl font-medium">Event Booking app</h1>
    <h2 class="text-2xl font-medium">All events</h2>
    <section class="grid grid-cols-2 gap-8">
      <template v-if="!eventsLoading">
        <EventCard
          v-for="event in events"
          :key="event.id"
          :title="event.title"
          :when="event.date"
          :description="event.description"
          @register="regHandler(event)"
        ></EventCard>
      </template>
      <template v-else>
        <LoadingEventCard v-for="i in 4" :key="i"></LoadingEventCard>
      </template>
    </section>
    <h2 class="text-2xl font-medium">Your Bookings</h2>
    <section class="grid grid-cols-1 gap-4">
      <template v-if="!bookingsLoading">
        <BookingItem
          v-for="booking in bookings"
          :key="booking.id"
          :event-title="booking.eventTitle"
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
import { onMounted, ref } from 'vue'
import EventCard from '@/components/EventCard.vue'
import BookingItem from './components/BookingItem.vue'
import LoadingEventCard from './components/LoadingEventCard.vue'
import LoadingBookingsCard from './components/LoadingBookingsCard.vue'
const events = ref([])
const bookings = ref([])
const eventsLoading = ref(false)
const bookingsLoading = ref(false)
async function regHandler(event) {
  const newBooking = {
    id: Date.now().toString(),
    userId: 1,
    eventId: event.id,
    eventTitle: event.title
  }
  await fetch('http://localhost:3001/bookings', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ ...newBooking, status: 'confirmed' })
  })
  await fetchBookings()
}
const fetchEvents = async () => {
  eventsLoading.value = true
  try {
    const response = await fetch('http://localhost:3001/events')
    events.value = await response.json()
  } finally {
    eventsLoading.value = false
  }
  // console.log(events.value)
}
async function fetchBookings() {
  bookingsLoading.value = true
  try {
    const response = await fetch('http://localhost:3001/bookings')
    bookings.value = await response.json()
  } finally {
    bookingsLoading.value = false
  }
}
onMounted(() => {
  fetchEvents()
  fetchBookings()
})
</script>
