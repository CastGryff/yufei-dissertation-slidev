<template>
  <div
    v-if="$nav.currentPage > 1"
    class="deck-progress-simple"
  >
    <div
      class="deck-progress-simple-fill"
      :style="{ width: `${Math.min($nav.currentPage, $nav.total) / $nav.total * 100}%` }"
    />
    <span
      v-for="page in [1, 7, 9, 15, 21, 33].filter(page => page <= $nav.total)"
      :key="page"
      class="deck-progress-simple-dot"
      :class="{ passed: Math.min($nav.currentPage, $nav.total) >= page }"
      :style="{ left: `${($nav.total <= 1 ? 0 : (page - 1) / ($nav.total - 1)) * 100}%` }"
    />
  </div>

  <div v-if="$nav.currentPage > 1" class="deck-page-number">
    <span>{{ String(Math.min($nav.currentPage, $nav.total)).padStart(2, '0') }}</span>
    <span class="deck-page-total"> / {{ String($nav.total).padStart(2, '0') }}</span>
  </div>
</template>
