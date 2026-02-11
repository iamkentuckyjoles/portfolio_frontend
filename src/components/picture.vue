<template>
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
      />
    </div>
  </div>
</template>
