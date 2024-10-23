<template>
  <SectionCard>
    <template #header>
      {{ title }}
    </template>
    {{ when }}
    <template #footer>
      <p>{{ description }}</p>
      <div class="flex justify-end">
        <RoundButton @click.stop="$emit('register')">{{ label }}</RoundButton>
      </div>
    </template>
  </SectionCard>
</template>
<script setup>
/*
console.log(
  'hmm so the beforecreate/Created hook has run the refs,computed and methods are available for child(EventCard)'
)
import { onMounted, onBeforeMount } from 'vue'
onMounted(() => {
  console.log('EventCard(Child) mounted')
})
onBeforeMount(() => {
  console.log('BeforeMount hook of EventCard(Child)')
})
  */
import SectionCard from './SectionCard.vue'
import RoundButton from './RoundButton.vue'
defineProps({
  title: {
    type: String,
    default: ''
  },
  when: {
    type: String,
    default: ''
  },
  description: {
    type: String,
    default: ''
  }
})
defineEmits(['register'])
const label = 'register'
</script>
