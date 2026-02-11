<template>
  <div class="min-h-screen flex flex-col gap-6 p-6 bg-base-100 relative">
    <!-- Row 1: Picture + Info side by side, very close and left-aligned -->
    <div class="flex flex-row items-start gap-4 justify-start">
      <Picture />
      <Info />
    </div>

    <!-- Row 2: 3 columns -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <!-- Column 1: TechStack + ContactForm stacked -->
      <div class="flex flex-col gap-4">
        <TechStack />
        <ContactForm />
      </div>

      <!-- Column 2: Projects -->
      <div>
        <Projects />
      </div>

      <!-- Column 3: Experiences -->
      <div>
        <Experiences />
      </div>
    </div>

    <!-- Mode toggle -->
    <div class="absolute top-4 right-4">
      <button 
        class="btn btn-circle btn-xs bg-black text-white"
        @click="toggleTheme"
      >
        {{ theme === 'light' ? '🌙' : '☀️' }}
      </button>
    </div>
  </div>
</template>


<script setup>
import { ref, onMounted } from 'vue'
import Picture from './components/picture.vue'
import Info from './components/info.vue'
import TechStack from './components/techstack.vue'
import Projects from './components/projects.vue'
import Experiences from './components/experiences.vue'

// Track theme state
const theme = ref('light')

onMounted(() => {
  document.documentElement.setAttribute('data-theme', theme.value)
})

function toggleTheme() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
  document.documentElement.setAttribute('data-theme', theme.value)
}
</script>
