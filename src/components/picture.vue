<template>
<<<<<<< HEAD
  <div class="card card-sm bg-base-200 shadow max-w-xs p-2 flex items-center justify-center">
    <div class="relative">
      <!-- Default profile picture -->
      <img 
        src="@/assets/light.png" 
        alt="Profile picture" 
        class="w-24 h-24 md:w-32 md:h-32 object-cover transition-opacity duration-300 hover:opacity-0"
      />
      <!-- Hover image -->
      <img 
        src="@/assets/light_hover.png" 
        alt="Profile hover picture" 
        class="w-24 h-24 md:w-32 md:h-32 object-cover absolute top-0 left-0 opacity-0 hover:opacity-100 transition-opacity duration-300"
=======
  <div class="card card-sm max-w-xs p-3 flex items-center justify-center ">
    <div class="relative">
      <!-- Default profile picture -->
      <img 
        :src="theme === 'light' ? light : dark" 
        alt="Profile picture" 
        class="w-32 h-32 object-cover transition-opacity duration-300 hover:opacity-0"
      />
      <!-- Hover image -->
      <img 
        :src="theme === 'light' ? lightHover : darkHover" 
        alt="Profile hover picture" 
        class="w-32 h-32 object-cover absolute top-0 left-0 opacity-0 hover:opacity-100 transition-opacity duration-300"
>>>>>>> 500b6ad (Initial clean commit: portfolio frontend)
      />
    </div>
  </div>
</template>
<<<<<<< HEAD
=======

<script setup>
import { defineProps } from 'vue'

// Import images properly
import light from '@/assets/light.png'
import lightHover from '@/assets/light_hover.png'
import dark from '@/assets/dark.png'
import darkHover from '@/assets/dark_hover.png'

// Accept theme from parent as a prop
const props = defineProps({
  theme: {
    type: String,
    default: 'light'
  }
})
</script>
>>>>>>> 500b6ad (Initial clean commit: portfolio frontend)
