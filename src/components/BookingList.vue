<template>
  <section class="grid grid-cols-1 gap-4">
    <template v-if="error">
      <ErrorCard :retry="fetchBookings"
        >Couldnt load events at this time please retry Again</ErrorCard
      >
    </template>
    <template v-else>
      <template v-if="!bookingsLoading">
        <BookingItem
          v-for="booking in bookings"
          :key="booking.id"
          :event-title="booking.eventTitle"
          :status="booking.status"
          @cancel="cancelHandler(booking.id)"
        />
      </template>
      <template v-else>
        <LoadingBookingsCard v-for="i in 4" :key="i" />
      </template>
    </template>
  </section>
</template>
<script setup>
import { onMounted } from 'vue'
import ErrorCard from './ErrorCard.vue'
import LoadingBookingsCard from '@/components/LoadingBookingsCard.vue'
import BookingItem from '@/components/BookingItem.vue'
import useBookings from '@/composables/useBookings'
const { bookings, bookingsLoading, error, fetchBookings, cancelHandler } = useBookings()
onMounted(() => {
  fetchBookings()
})
</script>
