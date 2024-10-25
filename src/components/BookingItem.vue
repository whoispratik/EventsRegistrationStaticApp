<template>
  <SectionCard
    ><template #bookingitem>
      <div class="flex justify-between">
        <div class="flex space-x-2">
          <div>{{ eventTitle }}</div>
          <div><component :is="icon" :class="{ 'animate-spin': pending }"></component></div>
        </div>
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
import { computed } from 'vue'
import SectionCard from './SectionCard.vue'
import RoundButton from './RoundButton.vue'
import { LoaderCircle, Check } from 'lucide-vue-next'
defineEmits(['cancel'])
const props = defineProps({ eventTitle: String, status: String })
const pending = computed(() => props.status === 'pending')
const icon = computed(() => (pending.value ? LoaderCircle : Check))
</script>
