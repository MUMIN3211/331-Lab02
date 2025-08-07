<script setup lang="ts">
import type { Student } from '@/types'
import { ref, onMounted } from 'vue'
import StudentService from '@/services/StudentService'
import StudentCard from '@/components/StudentCard.vue'

const students = ref<Student[]>([])

onMounted(() => {
  StudentService.getStudents()
    .then((response) => {
      console.log(response.data)
      students.value = response.data
    })
    .catch((error) => {
      console.log('There was an error!', error)
    })
})
</script>

<template>
  <div class="flex flex-col items-center py-8 px-4">
    <h1 class="text-2xl font-semibold text-gray-800 mb-6">Students</h1>
    
    <div class="flex flex-col items-center gap-4 w-full max-w-2xl">
      <StudentCard
        v-for="student in students"
        :key="student.id"
        :student="student"
      />
    </div>
  </div>
</template>
