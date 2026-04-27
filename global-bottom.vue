<template>
  <Progress
    v-if="$nav.currentPage > 1"
    class="deck-progress"
    position="bottom"
    :level="1"
    :height="8"
    thickness="2px"
    barColor="rgba(31, 95, 147, 0.62)"
    strokeColor="rgba(31, 95, 147, 0.42)"
    activeColor="#f7f9fb"
    opacity="0.88"
    transitionDuration="220ms"
  />

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
