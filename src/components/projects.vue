<template>
  <div class="p-2 bg-base-300 rounded-lg shadow-md">
    <div class="flex items-center justify-between mb-2">
      <h2 class="text-xs font-bold">Projects</h2>
      <!-- Next Arrow -->
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
           viewBox="0 0 24 24" class="cursor-pointer hover:scale-105 transition-transform"
           @click="nextProject">
        <path fill="currentColor" d="M12.6 12L8 7.4L9.4 6l6 6l-6 6L8 16.6z"/>
      </svg>
    </div>

    <!-- Container that switches between projects -->
    <div class="p-2 bg-base-300 rounded">
      <Project1 v-if="currentProject === 0" />
      <Project2 v-if="currentProject === 1" />
      <Project3 v-if="currentProject === 2" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Project1 from './projects/project1.vue'
import Project2 from './projects/project2.vue'
import Project3 from './projects/project3.vue'

const currentProject = ref(0)
const totalProjects = 3

function nextProject() {
  currentProject.value = (currentProject.value + 1) % totalProjects
}
</script>
