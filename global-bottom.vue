<script setup>
const mainTotal = 34
const sectionPages = [1, 7, 9, 15, 20, 32]
</script>

<template>
  <div
    v-if="$nav.currentPage > 1 && $nav.currentPage <= mainTotal"
    class="deck-progress-simple"
  >
    <div
      class="deck-progress-simple-fill"
      :style="{ width: `${Math.min($nav.currentPage, mainTotal) / mainTotal * 100}%` }"
    />
    <span
      v-for="page in sectionPages.filter(page => page <= mainTotal)"
      :key="page"
      class="deck-progress-simple-dot"
      :class="{ passed: $nav.currentPage >= page }"
      :style="{ left: `${(mainTotal <= 1 ? 0 : (page - 1) / (mainTotal - 1)) * 100}%` }"
    />
  </div>

  <div
    v-if="$nav.currentPage > 1"
    class="deck-page-number"
    :class="{ 'is-backup': $nav.currentPage > mainTotal }"
  >
    <template v-if="$nav.currentPage <= mainTotal">
      <span>{{ String($nav.currentPage).padStart(2, '0') }}</span>
      <span class="deck-page-total"> / {{ String(mainTotal).padStart(2, '0') }}</span>
    </template>
    <template v-else>
      <span>Backup {{ String($nav.currentPage - mainTotal).padStart(2, '0') }}</span>
    </template>
  </div>
</template>
