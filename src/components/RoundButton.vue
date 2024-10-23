<template>
  <button
    :class="['text-sm font-medium rounded-full px-3 py-1', variants[variant] ?? variants.default]"
  >
    <slot></slot>
  </button>
</template>
<script setup>
/*
console.log(
  'hmm so the beforecreate/Created hook has run the refs,computed and methods are available for RoundButton'
)
import { onMounted, onBeforeMount } from 'vue'
onMounted(() => {
  console.log('RoundButton mounted')
})
onBeforeMount(() => {
  console.log('BeforeMount hook of RoundButton')
})
  */
const variants = {
  default: 'border border-gray-200 hover:bg-gray-100',
  danger: 'bg-red-200 enabled:hover:bg-red-100 text-red-900'
}
defineProps({
  variant: {
    type: String,
    default: 'default'
  }
})
</script>
