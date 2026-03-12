<template>
  <div>
    <!-- Cursor trail overlay -->
    <CanvasCursor />

    <!-- Loading overlay -->
    <div v-if="loading" class="fixed inset-0 flex items-center justify-center bg-white z-50">
    <CanvasCursor />
      <h1 class="text-black text-2xl font-bold">
        {{ displayedText }}
      </h1>
    </div>

    <!-- Main portfolio content -->
    <div v-else class="min-h-screen flex flex-col gap-4 p-2 bg-base-100 relative">
      <!-- Row 1: parent grid with 3 columns -->
      <div class="grid grid-cols-1 md:grid-cols-3 xl:grid-cols-3 gap-2 items-start">
        <!-- Column 1: Picture + Info -->
        <div class="flex flex-row items-start gap-2">
          <Picture :theme="theme" />
          <Info />
        </div>

        <!-- Column 2–3 combined: child grid -->
        <div class="md:col-span-2 xl:col-span-2">
          <div class="grid grid-cols-1 md:grid-cols-4 xl:grid-cols-4 gap-4">
            <div class="md:col-span-3 xl:col-span-3">
              <div class="p-4 bg-base-200 rounded-lg shadow-md w-full">
                <Quotes />
              </div>
            </div>
            <div>
              <div class="p-4 bg-base-200 rounded-lg shadow-md w-full">
                <Weather />
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Row 2: 3 columns -->
      <div class="grid grid-cols-1 md:grid-cols-3 xl:grid-cols-3 gap-4">
        <div class="flex flex-col">
          <TechStack />
        </div>
        <div>
          <Projects />
        </div>
        <div class="flex flex-col gap-4">
          <Experiences />
          <!-- Chatbot removed from here -->
        </div>
      </div>

      <!-- Mode toggle + Chatbot together -->
      <div class="absolute top-4 right-4 flex flex-col gap-2 items-end">
        <!-- Mode toggle -->
        <button 
          class="btn btn-circle btn-xs flex items-center justify-center transition-colors duration-300 hover:scale-105 transition-transform"
          :class="theme === 'light' ? 'bg-black text-white' : 'bg-white text-black'"
          @click="toggleTheme"
        >
          <!-- Show moon icon when in light mode -->
          <svg v-if="theme === 'light'" xmlns="http://www.w3.org/2000/svg" 
               width="16" height="16" viewBox="0 0 20 20" fill="currentColor">
            <path d="M13.719 1.8A8.759 8.759 0 1 1 1.8 13.719c3.335 1.867 7.633 1.387 10.469-1.449c2.837-2.837 3.318-7.134 1.45-10.47"/>
          </svg>

          <!-- Show sun icon when in dark mode -->
          <svg v-else xmlns="http://www.w3.org/2000/svg" 
               width="16" height="16" viewBox="0 0 80 80" fill="currentColor">
            <g>
              <path d="M44.243 29.757a11.086 11.086 0 1 0-8.486 20.484a11.086 11.086 0 0 0 8.486-20.484"/>
              <path fill-rule="evenodd" d="m40 12l6.965 11.185l12.834-2.984l-2.984 12.834L68 40l-11.185 6.965l2.984 12.834l-12.834-2.984L40 68l-6.965-11.185l-12.834 2.984l2.984-12.834L12 40l11.185-6.965l-2.984-12.834l12.834 2.984zm5.39 14.986a14.087 14.087 0 1 1-10.78 26.028a14.087 14.087 0 0 1 10.78-26.028" clip-rule="evenodd"/>
            </g>
          </svg>
        </button>

        <!-- Chatbot -->
        <Chatbot :theme="theme" />
      </div>
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
import Quotes from './components/quotes.vue'
import Weather from './components/weather.vue'
import Chatbot from './components/chatbot.vue'
import CanvasCursor from './components/CanvasCursor.vue'  // ✅ Cursor trail overlay

// Theme state
const theme = ref('light')

// Loading overlay state
const loading = ref(true)
const displayedText = ref("")
const fullText = "Welcome to Kenth's Portfolio"
let index = 0

onMounted(() => {
  document.documentElement.setAttribute('data-theme', theme.value)

  const interval = setInterval(() => {
    if (index < fullText.length) {
      displayedText.value += fullText[index]
      index++
    } else {
      clearInterval(interval)
      setTimeout(() => {
        loading.value = false
      }, 500)
    }
  }, 100) // typing speed
})

function toggleTheme() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
  document.documentElement.setAttribute('data-theme', theme.value)
}
</script>

<style>
/* Optional fade-in effect for text */
h1 {
  transition: opacity 0.3s ease-in-out;
}
</style>
