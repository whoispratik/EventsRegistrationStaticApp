<template>
  <RoundedCard>
    <template v-if="$slots.header">
      <h3 class="p-4 font-medium text-xl border-b border-gray-200"><slot name="header"></slot></h3>
    </template>
    <template v-if="$slots.default">
      <p class="p-4 border-b border-gray-200"><slot></slot></p>
    </template>
    <template v-if="$slots.footer">
      <div class="p-4">
        <slot name="footer"></slot>
      </div>
    </template>
    <template v-if="$slots.bookingitem">
      <div class="p-4"><slot name="bookingitem"></slot></div>
    </template>
  </RoundedCard>
</template>

<script setup>
/*
console.log(
  'hmm so the beforecreate/Created hook has run the refs,computed and methods are available for grandchild(SectionCard)'
)
import { onMounted, onBeforeMount } from 'vue'
onMounted(() => {
  console.log('SectionCard(grandchild1) mounted')
})
onBeforeMount(() => {
  console.log('BeforeMount hook of SectionCard(grandchild1)')
})
  */
import RoundedCard from './RoundedCard.vue'
</script>
