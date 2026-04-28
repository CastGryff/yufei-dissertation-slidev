<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const currentTime = ref('')
let timer

function updateTime() {
  currentTime.value = new Intl.DateTimeFormat(undefined, {
    hour: 'numeric',
    minute: '2-digit',
  }).format(new Date())
}

onMounted(() => {
  updateTime()
  timer = window.setInterval(updateTime, 1000)
})

onUnmounted(() => {
  window.clearInterval(timer)
})
</script>

<template>
  <div v-if="$nav.currentPage > 1 && currentTime" class="deck-clock">
    {{ currentTime }}
  </div>
</template>
