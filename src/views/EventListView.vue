<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import EventInfo from '@/components/EventInfo.vue'
import type { Event } from '@/types'

import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService'

const events = ref<Event[]>([])

onMounted(() => {
  EventService.getEvents()
    .then((response) => {
      events.value = response.data
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
})
</script>

<template>
  <h1>Events For Good</h1>
  <!-- new element -->
  <div class="events">
    <div v-for="event in events" :key="event.id" class="event-block">
      <EventInfo :event="event" />
      <EventCard :event="event" />
    </div>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 40px;
}

.event-block {
  width: 350px;
  margin-bottom: 32px;
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
</style>
