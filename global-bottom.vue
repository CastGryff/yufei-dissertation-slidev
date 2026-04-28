<template>
  <div
    v-if="$nav.currentPage > 1"
    class="deck-progress-simple"
    :class="{ 'is-backup': $nav.currentPage > 38 }"
  >
    <div
      class="deck-progress-simple-fill"
      :style="{ width: `${Math.min($nav.currentPage, 38) / 38 * 100}%` }"
    />
    <span v-for="page in [1, 7, 9, 15, 21, 33, 37]" :key="page" class="deck-progress-simple-dot" :class="{ passed: Math.min($nav.currentPage, 38) >= page }" :style="{ left: `${(page - 1) / 37 * 100}%` }" />
  </div>

  <div v-if="$nav.currentPage > 1" class="deck-page-number">
    <template v-if="$nav.currentPage <= 38">
      <span>{{ String($nav.currentPage).padStart(2, '0') }}</span>
      <span class="deck-page-total"> / 38</span>
    </template>
    <template v-else>
      <span>Backup {{ String($nav.currentPage - 38).padStart(2, '0') }}</span>
    </template>
  </div>
</template>
