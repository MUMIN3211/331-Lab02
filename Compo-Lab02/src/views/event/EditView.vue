<script setup lang="ts">
import { defineProps, toRefs } from 'vue'
import { type Event } from '@/types'
import { useMessageStore } from '@/stores/message'
import { useRouter } from 'vue-router'

const props = defineProps<{
  event: Event
  id: string
}>()

const { event } = toRefs(props)
const router = useRouter()
const store = useMessageStore()

const goToDetail = () => {
  store.updateMessage('You successfully go to Detail page')
  setTimeout(() => {
    store.resetMessage()
  }, 3000)
  router.push({ name: 'event-detail-view', params: { od: props.event.id } }) // NOTE: typo in 'od'?
}
</script>

<template>
  <div class="flex flex-col items-start gap-4 p-4 bg-white border border-gray-200 rounded-md shadow-sm max-w-md">
    <p class="text-gray-700 text-base font-medium">Edit event here</p>
    <button
      @click="goToDetail"
      class="px-4 py-2 text-white bg-indigo-500 hover:bg-indigo-600 rounded-md text-sm font-medium transition"
    >
      Go to detail page
    </button>
  </div>
</template>
