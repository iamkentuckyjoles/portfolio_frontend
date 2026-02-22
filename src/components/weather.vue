<template>
  <div class="flex justify-center items-center min-h-[120px]">
    <!-- Weather tile -->
    <div v-if="weather" class="flex flex-col items-center text-center">
      <div>
        <img
          v-if="weather.icon_url"
          :src="weather.icon_url"
          alt="Weather icon"
          class="w-15 h-15"
        />
      </div>
      <div class="text-xs font-semibold">
        Today {{ weather.temp ? weather.temp.toFixed(1) + '°C' : '--' }}
      </div>
      <div class="text-xs">
        Currently building in {{ weather.location }}
      </div>
    </div>

    <!-- Loading state -->
    <div v-else class="text-xs text-center">
      <span class="loading loading-infinity loading-xl"></span>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const weather = ref(null)
const API_BASE = import.meta.env.VITE_API_BASE_URL

onMounted(async () => {
  try {
    const res = await fetch(`${API_BASE}/weather/villaba/`)
    const data = await res.json()
    weather.value = data
  } catch (err) {
    console.error('Failed to fetch weather:', err)
  }
})
</script>

<style scoped>
div {
  text-align: center;
}
</style>
