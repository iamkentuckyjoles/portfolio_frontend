<template>
  <div class="flex p-6 justify-center items-center min-h-[120px]">
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
      <p v-else key="loading" class="text-sm text-center">
        <span class="loading loading-infinity loading-xl"></span>
      </p>
    </transition>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue"

/* ✅ Accept quotes array from parent */
const props = defineProps({
  quotes: { type: Array, default: () => [] }
})

const currentIndex = ref(0)
const currentQuote = ref(null)
let intervalId = null

// ✅ Start rotation through quotes every minute
const startRotation = () => {
  intervalId = setInterval(() => {
    if (props.quotes.length > 0) {
      currentIndex.value = (currentIndex.value + 1) % props.quotes.length
      currentQuote.value = props.quotes[currentIndex.value]
    }
  }, 60000) // 60,000 ms = 1 minute
}

onMounted(() => {
  if (props.quotes.length > 0) {
    currentIndex.value = 0
    currentQuote.value = props.quotes[currentIndex.value]
    startRotation()
  }
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
