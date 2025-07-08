<script setup lang="ts">
import { ref, onMounted } from 'vue'
import StudentService from '@/services/StudentService'
import type { Student } from '@/types'

const students = ref<Student[]>([])

onMounted(() => {
  StudentService.getStudents()
    .then((response) => {
      students.value = response.data
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
})
</script>

<template>
  <h1>Student List</h1>
  <div class="students">
    <div v-for="student in students" :key="student.id" class="student-card">
      <img :src="student.image" :alt="student.name + ' ' + student.surname" class="student-image" />
      <h2>{{ student.name }} {{ student.surname }}</h2>
      <p><strong>Student ID:</strong> {{ student.studentId }}</p>
      <p><strong>GPA:</strong> {{ student.gpa }}</p>
      <p><strong>Pen Amount:</strong> {{ student.penAmount }}</p>
      <p class="student-description">{{ student.description }}</p>
    </div>
  </div>
</template>

<style scoped>
.students {
  display: flex;
  flex-wrap: wrap;
  gap: 24px;
  margin-top: 40px;
  justify-content: center;
}
.student-card {
  background: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  padding: 24px;
  width: 260px;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.student-image {
  width: 100px;
  height: 100px;
  object-fit: cover;
  border-radius: 50%;
  margin-bottom: 12px;
  background: #eee;
}

.student-description {
  margin-top: 12px;
  color: #555;
  font-size: 0.95em;
}
</style>
