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
import { onMounted, ref } from 'vue'
import EventCard from '@/components/EventCard.vue'
import BookingItem from './components/BookingItem.vue'
import LoadingEventCard from './components/LoadingEventCard.vue'
import LoadingBookingsCard from './components/LoadingBookingsCard.vue'
const events = ref([])
const bookings = ref([])
const eventsLoading = ref(false)
const bookingsLoading = ref(false)
const findBookingById = (id) => bookings.value.findIndex((b) => b.id === id)
async function regHandler(event) {
  if (bookings.value.some((booking) => booking.eventId === event.id && booking.userId === 1)) {
    alert('You are already registered for this event.')
    return
  }
  const newBooking = {
    id: Date.now().toString(),
    userId: 1,
    eventId: event.id,
    eventTitle: event.title,
    status: 'pending'
  }
  bookings.value.push(newBooking)
  try {
    const response = await fetch('http://localhost:3001/bookings', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ ...newBooking, status: 'confirmed' })
    })

    if (response.ok) {
      const index = findBookingById(newBooking.id) //bookings.value.findIndex((b) => b.id === newBooking.id)
      bookings.value[index] = await response.json() // updating the status to confirm
    } else {
      throw new Error('failed to confirm booking')
    }
  } catch (e) {
    console.log('failed to register for event', e)
    bookings.value = bookings.value.filter((b) => b.id !== newBooking.id)
  }
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
async function cancelHandler(id) {
  const index = findBookingById(id)
  const originalBooking = bookings.value[index]
  bookings.value.splice(index, 1)

  try {
    const response = await fetch(`http://localhost:3001/bookings/${id}`, {
      method: 'DELETE'
    })
    if (!response.ok) throw new Error('Booking could not be cancelled')
  } catch (e) {
    console.error(`Failed to cancel booking:`, e)
    bookings.value.splice(index, 0, originalBooking)
  }
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
