<template>
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
        <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
          <div class="md:col-span-3">
            <div class="p-4 w-full">
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
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <div class="flex flex-col gap-4">
        <TechStack />
        <ContactForm />
      </div>
      <div>
        <Projects />
      </div>
      <div class="flex flex-col gap-4">
        <Experiences />
        <!-- ❌ Chatbot removed from here -->
      </div>
    </div>

    <!-- Mode toggle + Chatbot together -->
    <div class="absolute top-4 right-4 flex flex-col gap-2 items-end">
      <!-- Mode toggle -->
      <button 
        class="btn btn-circle btn-xs bg-black text-white"
        @click="toggleTheme"
      >
        {{ theme === 'light' ? '🌙' : '☀️' }}
      </button>

      <!-- Chatbot -->
      <Chatbot :theme="theme" />
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
import Chatbot from './components/chatbot.vue' // 👈 Import your chatbot

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
