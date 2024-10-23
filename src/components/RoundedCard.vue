<template>
  <div class="border border-gray-200 bg-white rounded-md">
    <slot></slot>
  </div>
</template>
<script setup>
/*
console.log(
  'hmm so the beforecreate/Created hook has run the refs,computed and methods are available for grandchild2(RoundedCard)'
)
import { onMounted, onBeforeMount } from 'vue'
onMounted(() => {
  console.log('RoundedCard(granchild2) mounted')
})
onBeforeMount(() => {
  console.log('BeforeMount hook of RoundedCard(granchild2)')
})*/
</script>
