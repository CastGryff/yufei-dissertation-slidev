<template>
  <div v-if="$nav.currentPage > 1" class="deck-page-number">
    <template v-if="$nav.currentPage <= 52">
      <span>{{ String($nav.currentPage).padStart(2, '0') }}</span>
      <span class="deck-page-total"> / 52</span>
    </template>
    <template v-else>
      <span>Backup {{ String($nav.currentPage - 52).padStart(2, '0') }}</span>
    </template>
  </div>
</template>
