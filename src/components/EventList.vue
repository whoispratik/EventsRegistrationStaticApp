<template>
  <template v-if="error">
    <ErrorCard :retry="fetchEvents">Couldnt load Events at this time please try again</ErrorCard>
  </template>
  <template v-else>
    <template v-if="!eventsLoading">
      <template v-if="events.length">
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
        <div class="col-span-2 text-center text-gray-500">No events yet</div>
      </template>
    </template>
    <template v-else>
      <LoadingEventCard v-for="i in 4" :key="i"></LoadingEventCard>
    </template>
  </template>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import EventCard from './EventCard.vue'
import LoadingEventCard from './LoadingEventCard.vue'
import ErrorCard from './ErrorCard.vue'
import useBookings from '@/composables/useBookings'
const { regHandler } = useBookings()
const events = ref([])
const eventsLoading = ref(false)
const error = ref(null)
defineEmits(['register'])
const fetchEvents = async () => {
  eventsLoading.value = true
  error.value = null
  try {
    const response = await fetch('http://localhost:3001/events')
    events.value = await response.json()
  } catch (e) {
    error.value = e
  } finally {
    eventsLoading.value = false
  }
  // console.log(events.value)
}
onMounted(() => {
  fetchEvents()
})
</script>
