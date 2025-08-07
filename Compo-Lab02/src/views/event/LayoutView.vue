<script setup lang="ts">
import { useEventStore } from '@/stores/event'
import { storeToRefs } from 'pinia'

const store = useEventStore()
const { event } = storeToRefs(store)
</script>

<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <nav class = "py-6">
      <router-link class="font-bold text-grey-700" exact-active-class="text-green-500" :to="{ name: 'event-detail-view' }">Details</router-link>
      |
      <router-link class="font-bold text-grey-700" exact-active-class="text-green-500" :to="{ name: 'event-register-view' }">Register</router-link>
      |
      <router-link class="font-bold text-grey-700" exact-active-class="text-green-500" :to="{ name: 'event-edit-view' }">Edit</router-link>
    </nav>
    <router-view :event="event"></router-view>
  </div>
</template>
