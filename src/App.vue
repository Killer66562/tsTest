<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import { Course } from './models';
import { ref } from 'vue';

import axios from 'axios';

const courses = ref<Course[]>([]);

const getAllCourses = async () => {
  try {
    const response = await axios.get<Course[]>("https://ncuesaweb.ncue.edu.tw/DEAN-api/courses");
    courses.value = response.data;
  }
  catch (err) {
    console.error("Error");
  }
}

const filter = () => {
  courses.value = courses.value.filter((course) => {
    return course.id <= 500;
  });
}

getAllCourses();
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />

  <table>
    <thead>
      <tr>
        <th>ID</th>
        <th>開課ID</th>
        <th>課程中文名稱</th>
        <th>開課教師</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="course in courses" :key="course.id">
        <td>{{ course.id }}</td>
        <td>{{ course.course_id }}</td>
        <td>{{ course.course_zh_name }}</td>
        <td>{{ course.course_teacher_name }}</td>
      </tr>
    </tbody>
  </table>
  <button type="button" @click="filter">Filter</button>

</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
