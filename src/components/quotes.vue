<template>
  <div class="flex p-6 justify-center items-center min-h-[120px]">
    <transition name="fade" mode="out-in">
      <div v-if="quote" class="flex flex-col">
        <!-- Quote centered -->
        <p class="text-xs italic text-center">
          "{{ quote.message }}"
        </p>
        <!-- Author aligned to the right -->
        <p class="text-xs text-right mt-2">
          — {{ quote.author }}
        </p>
      </div>
      <p v-else key="loading" class="text-sm text-center">
        <span class="loading loading-infinity loading-xl"></span>
      </p>
    </transition>
  </div>
</template>

<script setup>
/* ✅ Accept quote data from parent instead of fetching */
const props = defineProps({
  quote: { type: Object, default: null }
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
