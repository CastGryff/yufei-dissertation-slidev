<template>
  <div v-if="$nav.currentPage > 1" class="deck-page-number">
    <template v-if="$nav.currentPage <= 50">
      <span>{{ String($nav.currentPage).padStart(2, '0') }}</span>
      <span class="deck-page-total"> / 50</span>
    </template>
    <template v-else>
      <span>Backup {{ String($nav.currentPage - 50).padStart(2, '0') }}</span>
    </template>
  </div>
</template>
