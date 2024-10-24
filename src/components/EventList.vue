<template>
  <template v-if="!eventsLoading">
    <template v-if="events.length">
      <EventCard
        v-for="event in events"
        :key="event.id"
        :title="event.title"
        :when="event.date"
        :description="event.description"
        @register="$emit('register', event)"
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

<script setup>
import { ref, onMounted } from 'vue'
import EventCard from './EventCard.vue'
import LoadingEventCard from './LoadingEventCard.vue'
const events = ref([])
const eventsLoading = ref(false)
defineEmits(['register'])
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
onMounted(() => {
  fetchEvents()
})
</script>
