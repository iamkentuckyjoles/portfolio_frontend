<template>
  <div class="flex justify-center items-center min-h-[120px]">
    <!-- Weather tile -->
    <div v-if="weather" class="flex flex-col items-center text-center">
      <!-- Weather Icon -->
      <div>
        <img
          v-if="weather.icon_url"
          :src="weather.icon_url"
          alt="Weather icon"
          class="w-15 h-15"
        />
      </div>

      <!-- Temperature -->
      <div class="text-xs font-semibold">
        Today {{ weather.temp ? weather.temp.toFixed(1) + '°C' : '--' }}
      </div>

      <!-- Location -->
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

onMounted(async () => {
  try {
    const res = await fetch('http://localhost:8001/api/weather/villaba/')
    const data = await res.json()
    weather.value = data
  } catch (err) {
    console.error('Failed to fetch weather:', err)
  }
})
</script>

<style scoped>
/* Ensure everything is centered */
div {
  text-align: center;
}
</style>
