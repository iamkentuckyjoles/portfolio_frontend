<template>
  <div class="p-4 bg-base-200 rounded-lg shadow-md">
    <h2 class="text-xs font-bold mb-2">My Tech Stack</h2>

    <!-- Frontend -->
    <h3 class="text-xs font-semibold mt-2">Frontend</h3>
    <div class="grid grid-cols-2 text-center sm:grid-cols-3 gap-2 text-xs">
      <div class="p-1 bg-base-300 rounded">TailwindCSS</div>
      <div class="p-1 bg-base-300 rounded">CSS</div>
      <div class="p-1 bg-base-300 rounded">JavaScript</div>
      <div class="p-1 bg-base-300 rounded">Vue.js</div>
    </div>

    <!-- Backend -->
    <h3 class="text-xs font-semibold mt-2">Backend</h3>
    <div class="grid grid-cols-2 text-center sm:grid-cols-3 gap-2 text-xs">
      <div class="p-1 bg-base-300 rounded">Python</div>
      <div class="p-1 bg-base-300 rounded">Django</div>
      <div class="p-1 bg-base-300 rounded">DRF</div>
      <div class="p-1 bg-base-300 rounded">Postgres</div>
    </div>

    <!-- DevOps & Cloud -->
    <h3 class="text-xs font-semibold mt-2">DevOps & Cloud</h3>
    <div class="grid grid-cols-2 text-center sm:grid-cols-3 gap-2 text-xs">
      <div class="p-1 bg-base-300 rounded">GitHub Actions</div>
      <div class="p-1 bg-base-300 rounded">DigitalOcean</div>
      <div class="p-1 bg-base-300 rounded">Vercel</div>
      <div class="p-1 bg-base-300 rounded">Docker</div>
    </div>
  </div>
</template>

<script setup>
// Static for now — later we can make this dynamic
</script>
