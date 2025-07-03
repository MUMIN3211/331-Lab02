<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import CategoryInfo from '@/components/CategoryInfo.vue'
import type { Event } from '@/types'
import { ref, onMounted } from 'vue'
import axios from 'axios'

const events = ref<Event[]>(null)
onMounted(() =>{
  axios
    .get('https://my-json-server.typicode.com/MUMIN3211/Lab02-Compo/db')
    .then(response => {
      console.log('Events fetched successfully:', response.data.events)
    })
    .catch(error => {
      console.error('Error fetching events:', error)
    })
})
</script>

<template>
  <h1>Events For Good</h1>
  <!-- new element -->
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
  <div class="category">
    <CategoryInfo v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.category {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
</style>