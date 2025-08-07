<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import CategoryInfo from '@/components/CategoryInfo.vue'
import { type Event } from '@/types'
import { ref, onMounted, computed, watchEffect } from 'vue'
import EventService from '@/services/EventService'

const events = ref<Event[] | null>([])
const totalEvents = ref(0)

const props = defineProps({
  page: {
    type: Number,
    required: true,
  },
  pageSize: {
    type: Number,
    required: true,
  },
})

const page = computed(() => props.page)
const pageSize = computed(() => props.pageSize)

const hasNexPage = computed(() => {
  const totalPages = Math.ceil(totalEvents.value / pageSize.value)
  return page.value < totalPages
})

const pageSizeOption = [2, 3, 4, 6]

onMounted(() => {
  watchEffect(() => {
    EventService.getEvents(pageSize.value, page.value)
      .then((response) => {
        events.value = response.data
        totalEvents.value = response.headers['x-total-count']
      })
      .catch((error) => {
        console.error('There was an error!', error)
      })
  })
})
</script>

<template>
  <!-- Page Size Selection -->
  <div class="flex justify-center gap-4 my-6">
    <router-link
      v-for="size in pageSizeOption"
      :key="size"
      :to="{ name: 'home', query: { page: 1, pageSize: size } }"
    >
      <button
        :class="[
          'px-3 py-1 rounded border text-sm font-medium transition-all duration-200',
          pageSize === size
            ? 'bg-emerald-500 text-white border-emerald-500'
            : 'bg-white text-gray-700 border-gray-300 hover:bg-gray-100',
        ]"
      >
        {{ size }} per page
      </button>
    </router-link>
  </div>

  <!-- Heading -->
  <h1 class="text-2xl font-semibold text-center text-gray-800 mb-6">Events For Good</h1>

  <!-- Events and Pagination -->
  <div class="flex flex-col items-center space-y-6">
    <EventCard v-for="event in events" :key="event.id" :event="event" />

    <div class="flex justify-between w-72 text-sm text-gray-600 font-medium">
      <router-link
        v-if="page !== 1"
        :to="{ name: 'home', query: { page: page - 1, pageSize: pageSize } }"
        class="hover:text-emerald-500 transition-colors"
      >
        &#60; Prev Page
      </router-link>
      <div></div>
      <router-link
        v-if="hasNexPage"
        :to="{ name: 'home', query: { page: page + 1, pageSize: pageSize } }"
        class="hover:text-emerald-500 transition-colors"
      >
        Next Page &#62;
      </router-link>
    </div>
  </div>

  <!-- Category Info Section -->
  <div class="flex flex-col items-end mt-10 space-y-4">
    <CategoryInfo v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>
