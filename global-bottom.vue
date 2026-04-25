<template>
  <div v-if="$nav.currentPage > 1" class="deck-page-number">
    <span>{{ String($nav.currentPage).padStart(2, '0') }}</span>
    <span class="deck-page-total"> / {{ String($nav.total).padStart(2, '0') }}</span>
  </div>
</template>
