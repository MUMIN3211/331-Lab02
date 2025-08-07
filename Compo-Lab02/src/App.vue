<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { useMessageStore } from './stores/message'
import { storeToRefs } from 'pinia'

const store = useMessageStore()
const { message } = storeToRefs(store)
</script>

<template>
  <div class="font-sans text-gray-800 antialiased min-h-screen bg-gray-50 flex flex-col items-center ">
    <!-- Header -->
    <header class="w-full bg-white shadow-sm py-4 px-6">
      
      <!-- Flash Message -->
      <div
        v-if="message"
        class="mb-4 mx-auto max-w-xl rounded-md border border-green-300 bg-green-100 text-green-800 text-center py-2 px-4 animate-fade-in-down"
      >
        <h4 class="text-sm font-medium">{{ message }}</h4>
      </div>
      <h1>Deploy with vercel</h1>
      <!-- Nav -->
      <nav class="flex justify-center gap-6 text-sm sm:text-base">
        <RouterLink
          :to="{ name: 'home' }"
          class="relative font-semibold text-gray-700 hover:text-emerald-500 transition-colors duration-200 after:absolute after:-bottom-1 after:left-0 after:h-0.5 after:w-0 hover:after:w-full after:bg-emerald-400 after:transition-all after:duration-300"
        >
          Event
        </RouterLink>

        <RouterLink
          :to="{ name: 'about' }"
          class="relative font-semibold text-gray-700 hover:text-emerald-500 transition-colors duration-200 after:absolute after:-bottom-1 after:left-0 after:h-0.5 after:w-0 hover:after:w-full after:bg-emerald-400 after:transition-all after:duration-300"
        >
          About
        </RouterLink>

        <RouterLink
          :to="{ name: 'students' }"
          class="relative font-semibold text-gray-700 hover:text-emerald-500 transition-colors duration-200 after:absolute after:-bottom-1 after:left-0 after:h-0.5 after:w-0 hover:after:w-full after:bg-emerald-400 after:transition-all after:duration-300"
        >
          Students
        </RouterLink>
      </nav>
    </header>

    <!-- Main Content -->
    <main class="w-full max-w-4xl px-4 py-8">
      <RouterView />
    </main>

    
  </div>
</template>
