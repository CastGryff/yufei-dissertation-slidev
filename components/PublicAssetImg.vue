<script setup>
import { computed } from 'vue'

const props = defineProps({
  path: {
    type: String,
    required: true,
  },
  alt: {
    type: String,
    default: '',
  },
})

const src = computed(() => `${import.meta.env.BASE_URL}${props.path.replace(/^\/+/, '')}`)
</script>

<template>
  <img :src="src" :alt="alt">
</template>
