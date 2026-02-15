<template>
  <div class="flex justify-center items-center min-h-[120px]">
    <!-- Weather tile -->
    <div v-if="weather" class="flex flex-col items-center gap-2 text-center">
      <!-- Emoji (depends on condition) -->
      <div class="text-2xl">
        {{ getEmoji(weather.description) }}
      </div>

      <!-- Temperature -->
      <div class="text-xs font-semibold">
        Today {{ weather.temp ? weather.temp.toFixed(1) + '°C' : '--' }}
      </div>

      <!-- Location -->
      <div class="text-xs">
        Building from {{ weather.location }}
      </div>

    </div>

    <!-- Loading state -->
    <div v-else class="text-xs text-center">
      Loading weather...
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const weather = ref(null)

onMounted(async () => {
  try {
    const res = await fetch('http://localhost:8001/api/weather/villaba/')
    const data = await res.json()
    weather.value = data
  } catch (err) {
    console.error('Failed to fetch weather:', err)
  }
})

// Map backend condition/description to emoji
function getEmoji(description) {
  if (!description) return '❓'
  const desc = description.toLowerCase()
  if (desc.includes('clear')) return '☀️'
  if (desc.includes('cloud')) return '☁️'
  if (desc.includes('rain')) return '🌧️'
  if (desc.includes('drizzle')) return '🌦️'
  if (desc.includes('thunder')) return '⛈️'
  if (desc.includes('snow')) return '❄️'
  return '🌤️'
}
</script>

<style scoped>
/* Ensure everything is centered */
div {
  text-align: center;
}
</style>
