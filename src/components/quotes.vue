<template>
  <div class="p-6">
    <transition name="fade" mode="out-in">
      <div v-if="currentQuote" :key="currentIndex" class="flex flex-col">
        <!-- Quote centered -->
        <p class="text-xs italic text-center">
          "{{ currentQuote.message }}"
        </p>
        <!-- Author aligned to the right -->
        <p class="text-xs text-right mt-2">
          — {{ currentQuote.author }}
        </p>
      </div>
      <p v-else key="loading" class="text-sm text-gray-500 text-center">Loading...</p>
    </transition>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue"

const quotes = ref([])
const currentIndex = ref(0)
const currentQuote = ref(null)
let intervalId = null

// Fetch quotes from Django API
const fetchQuotes = async () => {
  try {
    const res = await fetch("http://localhost:8001/api/quotes/")
    let data = await res.json()

    // Sort by id ascending (1 → 60)
    data.sort((a, b) => a.id - b.id)

    quotes.value = data

    if (quotes.value.length > 0) {
      currentIndex.value = 0
      currentQuote.value = quotes.value[currentIndex.value]
    }
  } catch (err) {
    console.error("Failed to fetch quotes:", err)
  }
}

// Cycle through quotes every minute
const startRotation = () => {
  intervalId = setInterval(() => {
    if (quotes.value.length > 0) {
      currentIndex.value = (currentIndex.value + 1) % quotes.value.length
      currentQuote.value = quotes.value[currentIndex.value]
    }
  }, 60000) // 60,000 ms = 1 minute
}

onMounted(async () => {
  await fetchQuotes()
  startRotation()
})

onUnmounted(() => {
  if (intervalId) clearInterval(intervalId)
})
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
