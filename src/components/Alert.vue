<script setup>
import { computed } from 'vue'

const props = defineProps({
  alert: {
    type: Object,
    required: true
  }
})

const isError = computed(() => props.alert.type === 'error')

</script>

<template>
  <div :class="[isError ? 'bg-red-100 border-red-400 text-red-700' : 'bg-green-100 border-green-400 text-green-700']"
    class="fixed flex items-center justify-center gap-3 p-2 border top-10 right-10">
    <svg v-if="isError" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
      stroke="currentColor" class="w-6 h-6">
      <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
    </svg>
    <svg v-else xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
      stroke="currentColor" class="w-6 h-6">
      <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
    </svg>
    <p>{{ alert.message }}</p>
  </div>
</template>