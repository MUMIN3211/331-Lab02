<script setup lang="ts">
import { type Event } from '@/types'

defineProps<{
  event: Event
}>()
</script>

<template>
  <router-link
    :to="{ name: 'event-detail-view', params: { id: event.id } }"
    class="no-underline text-gray-800"
  >
    <div
      class="border border-gray-500 p-5 w-[250px] mb-5 cursor-pointer rounded-md transition-transform duration-200 ease-in-out hover:scale-105 hover:shadow-md bg-white"
    >
      <h2 class="text-lg font-semibold mb-1">{{ event.title }}</h2>
      <span class="text-sm text-gray-600 block">
        @{{ event.time }} on {{ event.date }}
      </span>
    </div>
  </router-link>
</template>
