<template>
  <SectionCard>
    <template #retry>
      <div class="space-y-4 items-center flex flex-col">
        <div class="text-red-500"><slot></slot></div>
        <RoundButton @click="retry">Retry now</RoundButton>
      </div>
    </template>
  </SectionCard>
</template>
<script setup>
import SectionCard from './SectionCard.vue'
import RoundButton from './RoundButton.vue'
defineProps({
  retry: {
    type: Function,
    Required: false
  }
})
</script>
