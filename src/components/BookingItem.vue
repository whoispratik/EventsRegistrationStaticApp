<template>
  <SectionCard
    ><template #bookingitem>
      <div class="flex justify-between">
        <div>{{ eventTitle }}</div>
        <RoundButton variant="danger" @click.stop="$emit('cancel')"> Cancel</RoundButton>
      </div>
    </template>
  </SectionCard>
</template>
<script setup>
/*
console.log(
  'hmm so the beforecreate/Created hook has run the refs,computed and methods are available for child(BookingItem)'
)
import { onMounted, onBeforeMount } from 'vue'
onMounted(() => {
  console.log('BookingItem(Child) mounted')
})
onBeforeMount(() => {
  console.log('BeforeMount hook of BookingItem(Child)')
})
  */
import SectionCard from './SectionCard.vue'
import RoundButton from './RoundButton.vue'
defineEmits(['cancel'])
defineProps({ eventTitle: String })
</script>
