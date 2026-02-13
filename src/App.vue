<template>
<<<<<<< HEAD
  <div class="min-h-screen flex flex-col gap-6 p-6 bg-base-100 relative">
    <!-- Row 1: Picture + Info side by side, very close and left-aligned -->
    <div class="flex flex-row items-start gap-4 justify-start">
      <Picture />
      <Info />
=======
  <div class="min-h-screen flex flex-col gap-4 p-2 bg-base-100 relative">
    <!-- Row 1: parent grid with 3 columns -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8 items-start">
      <!-- Column 1: Picture + Info -->
      <div class="flex flex-row items-start gap-2">
        <Picture :theme="theme" />
        <Info />
      </div>

      <!-- Column 2–3 combined: child grid -->
      <div class="md:col-span-2">
        <!-- Child grid: 4 columns -->
        <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
          <!-- Child columns 1–3 combined: Quotes -->
          <div class="md:col-span-3">
            <div class="p-4 w-full">
              <Quotes />
            </div>
          </div>

          <!-- Child column 4: Weather -->
          <div>
            <div class="p-4 bg-base-200 rounded-lg shadow-md w-full">
              <Weather />
            </div>
          </div>
        </div>
      </div>
>>>>>>> 500b6ad (Initial clean commit: portfolio frontend)
    </div>

    <!-- Row 2: 3 columns -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <!-- Column 1: TechStack + ContactForm stacked -->
      <div class="flex flex-col gap-4">
        <TechStack />
        <ContactForm />
      </div>

      <!-- Column 2: Projects -->
<<<<<<< HEAD
      <div>
        <Projects />
      </div>

      <!-- Column 3: Experiences -->
      <div>
        <Experiences />
      </div>
=======
      <Projects />

      <!-- Column 3: Experiences -->
      <Experiences />
>>>>>>> 500b6ad (Initial clean commit: portfolio frontend)
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

<<<<<<< HEAD

=======
>>>>>>> 500b6ad (Initial clean commit: portfolio frontend)
<script setup>
import { ref, onMounted } from 'vue'
import Picture from './components/picture.vue'
import Info from './components/info.vue'
import TechStack from './components/techstack.vue'
import Projects from './components/projects.vue'
import Experiences from './components/experiences.vue'
<<<<<<< HEAD

// Track theme state
const theme = ref('light')

onMounted(() => {
  document.documentElement.setAttribute('data-theme', theme.value)
})

=======
import Quotes from './components/quotes.vue'
import Weather from './components/weather.vue'

const theme = ref('light')
onMounted(() => {
  document.documentElement.setAttribute('data-theme', theme.value)
})
>>>>>>> 500b6ad (Initial clean commit: portfolio frontend)
function toggleTheme() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
  document.documentElement.setAttribute('data-theme', theme.value)
}
</script>
