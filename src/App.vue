<template>
  <main class="mx-auto my-8 space-y-8">
    <h1 class="text-4xl font-medium">Event Booking app</h1>
    <h2 class="text-2xl font-medium">All events</h2>
    <section class="grid grid-cols-2 gap-8">
      <EventList></EventList>
    </section>
    <h2 class="text-2xl font-medium">Your Bookings</h2>
    <BookingList></BookingList>
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
import BookingList from './components/BookingList.vue'
import EventList from './components/EventList.vue'
</script>
