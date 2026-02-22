<template>
  <div class="p-3 bg-base-300 rounded-lg shadow-md">
    <h2 class="text-xs font-bold">Tech Stack</h2>

    <!-- Backend -->
    <h3 class="text-xs text-center font-medium mt-1"> Backend</h3>
    <div class="grid grid-cols-2 text-center sm:grid-cols-3 gap-2 text-xs p-1">
      <div class="p-1 text-white rounded bg-gradient-to-r from-blue-700 to-yellow-500">
        Python
      </div>
      <div class="p-1 text-white bg-green-700 rounded">Django</div>
      <div class="p-1 text-white rounded bg-gradient-to-r from-white via-red-500 to-black">
        DRF
      </div>
      <div class="p-1 text-white bg-blue-700 rounded">Postgres</div>
      <div class="p-1 text-white rounded bg-gradient-to-r from-blue-700 to-orange-500">
        MySQL
      </div>
    </div>

    <!-- Frontend -->
    <h3 class="text-xs text-center font-medium mt-1"> Frontend</h3>
    <div class="grid grid-cols-2 text-center sm:grid-cols-3 gap-2 text-xs p-1">
      <div class="p-1 text-white bg-blue-500 rounded">TailwindCSS</div>
      <div class="p-1 text-white bg-yellow-500 rounded">JavaScript</div>
      <div class="p-1 text-white rounded bg-gradient-to-r from-blue-900 to-green-600">
        Vue.js
      </div>
    </div>

    <!-- DevOps & Cloud -->
    <h3 class="text-xs text-center font-medium mt-1">DevOps & Cloud</h3>
    <div class="grid grid-cols-2 text-center sm:grid-cols-3 gap-2 text-xs p-1">
      <div class="p-1 bg-gray-700 text-white rounded">GitHub Actions</div>
      <div class="p-1 text-white rounded bg-gradient-to-r from-black to-yellow-500">AWS</div>
      <div class="p-1 bg-blue-500 text-white rounded">DigitalOcean</div>
      <div class="p-1 bg-black text-white rounded">Vercel</div>
      <div class="p-1 bg-blue-700 text-white rounded">Docker</div>
    </div>

    <!-- Tools & Communication -->
    <h3 class="text-xs font-semibold mt-1">Tools & Communication</h3>
    <div class="grid grid-cols-2 text-center sm:grid-cols-3 gap-2 text-xs p-1">
     <div class="p-1 rounded text-white bg-gradient-to-r from-pink-400 via-blue-400 via-green-400 to-yellow-400">
        Slack
      </div>
      <div class="p-1 bg-blue-800 text-white rounded">Discord</div>
      <div class="p-1 text-white bg-gradient-to-r from-blue-800 to-purple-800 rounded">Canva</div>
      <div class="p-1 text-white rounded text-white bg-gradient-to-r from-purple-400 from-pink-400 via-blue-400 via-yellow-400 to-green-400">
        Microsoft 365
      </div>
      <div class="p-1 text-white bg-gradient-to-r from-blue-800 to-blue-400 rounded">Photoshop</div>
    </div>

    <!-- Operating Systems -->
    <h3 class="text-xs font-semibold mt-1">Operating Systems</h3>
    <div class="grid grid-cols-2 text-center sm:grid-cols-3 gap-2 text-xs p-1">
      <div class="p-1 text-white bg-orange-600 rounded">Linux (Ubuntu)</div>
      <div class="p-1 text-white bg-blue-500 rounded">Windows</div>
    </div>

    <!-- Environment & Hardware -->
    <h3 class="text-xs font-semibold mt-1">Environment & Hardware</h3>
    <div class="grid grid-cols-2 text-center sm:grid-cols-3 gap-2 text-xs p-1">
      <div class="p-1 text-white bg-gray-500 rounded">100 Mbps WLAN</div>
      
      <!-- Group both Lenovo devices in one column -->
      <div class="p-1 text-white bg-gray-500 rounded">
        Lenovo i5 & Ryzen 5
      </div>
      <div class="p-1 text-white bg-gray-500 rounded">Powerbank 4000 mAh</div>
</div>

  </div>
</template>

<script setup>
// Static for now — later we can make this dynamic
</script>