<script setup lang="ts">
import type { Event } from '@/types'
defineProps<{ event: Event }>()
</script>

<template>
  <div class="event-info">
    <span class="category">{{ event.category }}</span>
    <span class="organizer">{{ event.organizer }}</span>
  </div>
</template>

<style scoped>
.event-info {
  text-align: right;
  margin-bottom: 4px;
}
.category,
.organizer {
  display: block;
  font-size: 0.98rem;
  color: #6c7a89;
  line-height: 1.2;
}
.category {
  font-weight: 500;
}
.organizer {
  font-style: italic;
}
</style>
