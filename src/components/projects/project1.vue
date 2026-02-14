<template>
  <div class="bg-base-300 rounded text-xs">
    <!-- Slide container -->
    <div class="w-full rounded overflow-hidden relative">
      <transition name="fade" mode="out-in">
        <div :key="currentSlide" class="w-full">
          <img
            :src="slides[currentSlide].src"
            class="w-full"
            :alt="slides[currentSlide].alt"
          />
        </div>
      </transition>
    </div>

    <!-- Dot navigation -->
    <div class="flex w-full justify-center gap-2 mt-1">
      <span
        v-for="(slide, index) in slides"
        :key="'dot-' + index"
        class="w-3 h-3 rounded-full cursor-pointer"
        :class="currentSlide === index ? 'bg-gray-800' : 'bg-gray-400'"
        @click="goToSlide(index)"
      ></span>
    </div>

   <!-- Project details -->
    <h3 class="font-semibold mt-1">XMP Filter Storage</h3>
    <p>
      A secure web app for freelance photo editors to strictly manage and track XMP files.
      Includes role-based dashboards, Editors Log, tutorials per role, ranking system,
      notifications, announcements, profile picture upload, and strict XMP file storage.
    </p>
    <!-- Tech Stack -->
    <p class="mt-1 font-semibold">Tech Stack Used:</p>
    <div class="flex items-center gap-3 mt-1">
      <!-- Django -->
      <div class="flex items-center gap-1 mt-1">
        <!-- SVG Django -->
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 256 256">
            <g fill="none">
                <rect width="256" height="256" fill="#092e20" rx="60"/>
                <path fill="#fff" d="M112.689 51h28.615v132.45c-14.679 2.787-25.456 3.902-37.161 3.902C69.209 187.351 51 171.559 51 141.271c0-29.173 19.325-48.124 49.24-48.124c4.645 0 8.175.37 12.449 1.485zm0 66.671c-3.344-1.113-6.131-1.485-9.661-1.485c-14.493 0-22.856 8.919-22.856 24.526c0 15.238 7.991 23.599 22.67 23.599c3.157 0 5.76-.186 9.847-.742z"/>
                <path fill="#fff" d="M186.826 95.19v66.332c0 22.856-1.672 33.818-6.689 43.295c-4.646 9.106-10.778 14.865-23.413 21.183l-26.571-12.636c12.635-5.945 18.767-11.146 22.668-19.139c4.089-8.175 5.391-17.652 5.391-42.55V95.189zm-28.614-44.038h28.614V80.51h-28.614z"/>
            </g>
        </svg>
        <span>Django</span>
      </div>
      <!-- DaisyUI -->
      <div class="flex items-center gap-1 mt-1">
        <!-- SVG DaisyUI -->
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 256 256">
            <defs>
            <radialGradient id="SVGGB36AbIe" cx="-.044%" cy="-.044%" r="141.466%" fx="-.044%" fy="-.044%">
                <stop offset="0%" stop-color="#ffe600"/>
                <stop offset="100%" stop-color="#ffa573"/>
            </radialGradient>
            </defs>
            <g opacity="0.7">
            <path fill="#ffd819" d="M84.315 22.535c-3.267 4.812-5.864 10.394-7.575 16.748A53.08 53.08 0 0 1 39.283 76.74c-6.353 1.71-11.936 4.307-16.748 7.575c-6.82-35.674 26.106-68.6 61.78-61.78"/>
            <path fill="#ffe029" d="M22.536 84.314c1.092 5.713 3.204 11.497 6.486 17.199a53.08 53.08 0 0 1 0 52.973c-3.283 5.702-5.394 11.485-6.486 17.198c-30.048-20.402-30.048-66.967 0-87.37"/>
            <path fill="#ffc141" d="M84.315 233.463c-3.267-4.811-5.864-10.394-7.575-16.747a53.08 53.08 0 0 0-37.457-37.458c-6.353-1.71-11.936-4.307-16.748-7.575c-6.82 35.674 26.106 68.6 61.78 61.78"/>
            <path fill="#ffb655" d="M171.685 233.463c-5.713-1.092-11.496-3.204-17.198-6.486a53.08 53.08 0 0 0-52.973 0c-5.702 3.282-11.486 5.394-17.199 6.486c20.403 30.048 66.968 30.048 87.37 0"/>
            <path fill="#ffb35b" d="M233.465 171.684c-4.812 3.268-10.394 5.863-16.748 7.574a53.08 53.08 0 0 0-37.457 37.458c-1.71 6.353-4.307 11.936-7.575 16.747c35.673 6.82 68.6-26.106 61.78-61.78"/>
            <path fill="#ffb656" d="M233.465 84.315c-1.093 5.713-3.204 11.496-6.487 17.198a53.09 53.09 0 0 0 0 52.973c3.283 5.702 5.394 11.485 6.487 17.198c30.047-20.402 30.047-66.966 0-87.37"/>
            <path fill="#ffc042" d="M171.685 22.535c3.268 4.812 5.864 10.394 7.575 16.748a53.09 53.09 0 0 0 37.457 37.457c6.354 1.71 11.936 4.307 16.748 7.574c6.82-35.673-26.107-68.599-61.78-61.78"/>
            <path fill="#ffce2a" d="M84.315 22.535c5.713 1.093 11.496 3.204 17.199 6.487a53.08 53.08 0 0 0 52.972 0c5.703-3.283 11.486-5.394 17.199-6.487c-20.403-30.047-66.967-30.047-87.37 0"/>
            </g>
            <path fill="url(#SVGGB36AbIe)" d="M76.742 39.282c1.71-6.353 4.307-11.935 7.575-16.747c5.712 1.092 11.496 3.204 17.197 6.486a53.08 53.08 0 0 0 52.973 0c5.702-3.283 11.486-5.394 17.199-6.486c3.267 4.812 5.864 10.394 7.574 16.747a53.08 53.08 0 0 0 37.458 37.458c6.353 1.71 11.935 4.307 16.747 7.574c-1.092 5.713-3.203 11.497-6.487 17.198a53.09 53.09 0 0 0 0 52.974c3.284 5.701 5.395 11.485 6.487 17.198c-4.812 3.268-10.394 5.863-16.747 7.574a53.08 53.08 0 0 0-37.458 37.458c-1.71 6.353-4.307 11.936-7.574 16.747c-5.713-1.092-11.497-3.203-17.199-6.486a53.09 53.09 0 0 0-52.973 0c-5.701 3.283-11.485 5.394-17.197 6.486c-3.268-4.811-5.865-10.394-7.575-16.747a53.08 53.08 0 0 0-37.458-37.458c-6.353-1.71-11.935-4.307-16.747-7.575c1.092-5.712 3.203-11.496 6.486-17.197a53.09 53.09 0 0 0 0-52.974c-3.283-5.701-5.394-11.484-6.486-17.197c4.811-3.268 10.394-5.864 16.747-7.575a53.08 53.08 0 0 0 37.458-37.458"/>
        </svg>
        <span>DaisyUI</span>
      </div>
      <!-- PostgreSQL -->
      <div class="flex items-center gap-1 mt-1">
        <!-- SVG PostgreSQL -->
        <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 256 256">
            <g fill="none">
            <rect width="256" height="256" fill="#242938" rx="60"/>
            <path fill="#336791" d="M203.48 148.688c-20.32 4.19-21.796-2.693-21.796-2.693c21.466-31.852 30.445-72.282 22.696-82.175c-21.121-27-57.691-14.224-58.303-13.893l-.197.035a72.5 72.5 0 0 0-13.563-1.414c-9.197-.14-16.172 2.412-21.473 6.427c0 0-65.236-26.873-62.199 33.8c.647 12.909 18.493 97.734 39.797 72.07c7.847-9.436 15.37-17.361 15.37-17.361c3.727 2.482 8.206 3.748 12.896 3.291l.365-.309a14.2 14.2 0 0 0 .148 3.642c-5.484 6.131-3.867 7.207-14.836 9.464c-11.095 2.285-4.57 6.356-.323 7.425c5.161 1.294 17.1 3.122 25.172-8.17l-.324 1.286c2.152 1.723 3.656 11.201 3.403 19.793c-.253 8.593-.422 14.485 1.266 19.097s3.375 14.977 17.789 11.953c12.045-2.58 18.281-9.281 19.16-20.432c.619-7.932 2.011-6.765 2.11-13.852l1.125-3.361c1.286-10.758.21-14.224 7.628-12.607l1.807.162c5.464.246 12.615-.879 16.805-2.827c9.035-4.19 14.393-11.194 5.484-9.351z"/>
            <path stroke="#fff" stroke-linecap="round" stroke-linejoin="round" stroke-width="5.034" d="M146.07 48.596c-2.25.703 36.31-14.097 58.233 13.908c7.735 9.893-1.23 50.323-22.697 82.174m-53.508 9.106c-.562 20.011.141 40.162 2.096 45c1.954 4.837 6.152 14.414 20.573 11.334c12.045-2.58 16.432-7.58 18.331-18.612l4.45-35.275zM110.816 53.469S45.537 26.779 48.575 87.45c.647 12.909 18.492 97.734 39.797 72.07c7.776-9.373 14.808-16.706 14.808-16.706z"/>
            <path stroke="#fff" stroke-linecap="round" stroke-linejoin="bevel" stroke-width="5.034" d="M181.613 144.664s1.407 6.891 21.797 2.686c8.909-1.842 3.544 5.161-5.484 9.352c-7.411 3.445-24.033 4.324-24.307-.422c-.703-12.27 8.747-8.543 8.065-11.616c-.619-2.77-4.852-5.484-7.636-12.262c-2.44-5.907-33.469-51.258 8.606-44.53c1.547-.316-10.969-40.077-50.344-40.654s-38.13 48.41-38.13 48.41"/>
            <path stroke="#fff" stroke-linejoin="round" stroke-width="5.034" d="M117.08 148.869c-5.484 6.131-3.867 7.207-14.835 9.464c-11.096 2.285-4.57 6.356-.324 7.425c5.161 1.294 17.1 3.122 25.172-8.178c2.461-3.445-.014-8.929-3.389-10.321c-1.631-.675-3.811-1.519-6.609 1.617z"/>
            <path stroke="#fff" stroke-linecap="round" stroke-linejoin="round" stroke-width="5.034" d="M116.722 148.763c-.563-3.607 1.181-7.889 3.044-12.909c2.799-7.523 9.254-15.047 4.093-38.932c-3.846-17.79-29.672-3.706-29.672-1.294s1.167 12.235-.422 23.66c-2.088 14.921 9.492 27.535 22.823 26.248"/>
            <path fill="#fff" stroke="#fff" stroke-width="1.68" d="M110.577 95.27c-.12.822 1.511 3.023 3.628 3.318c2.116.296 3.923-1.42 4.043-2.25c.119-.83-1.512-1.73-3.628-2.025s-3.938.14-4.043.956Z"/>
            <path fill="#fff" stroke="#fff" stroke-width="0.837" d="M175.011 93.59c.112.822-1.512 3.022-3.628 3.318c-2.117.295-3.938-1.42-4.043-2.25c-.106-.83 1.512-1.73 3.628-2.025s3.937.14 4.043.956Z"/>
            <path stroke="#fff" stroke-linecap="round" stroke-linejoin="round" stroke-width="5.034" d="M182.577 87.887c.351 6.469-1.393 10.863-1.618 17.747c-.323 9.998 4.768 21.445-2.904 32.906"/>
            </g>
        </svg>
        <span>PostgreSQL</span>
      </div>
      <!-- DigitalOcean -->
      <div class="flex items-center gap-1 mt-1">
        <!-- SVG DigitalOcean -->
        <svg xmlns="http://www.w3.org/2000/svg" width="25" height="25" viewBox="0 0 256 256">
            <path fill="#0080ff" d="M128 206.55v49.448c83.813 0 149.07-80.968 121.653-168.793c-11.981-38.38-42.478-68.877-80.858-80.858C80.97-21.069 0 44.19 0 128.001h49.561c.008 0 .013-.014.013-.014c.008-52.597 52.061-93.262 107.36-73.196c20.487 7.435 36.829 23.773 44.268 44.259c20.069 55.266-20.535 107.3-73.088 107.374v-49.288l-.009-.003H78.697c-.005 0-.01.007-.01.007v49.41zm-49.32 37.977H40.715l-.01-.009V206.55h37.982v37.968s-.005.009-.009.009M40.732 206.55H8.908c-.013 0-.023-.008-.023-.008v-31.81s.01-.024.023-.024H40.71c.013 0 .023.01.023.01z"/>
        </svg>
        <span>DigitalOcean</span>
      </div>
    </div>

    <!-- Links -->
    <p class="mt-2 flex items-center gap-4">
    <!-- GitHub Link -->
    <a href="https://github.com/iamkentuckyjoles/sif" 
      target="_blank" 
      class="flex items-center gap-1 text-blue-600 underline">
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" 
          viewBox="0 0 24 24" fill="none" stroke="currentColor" 
          stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
        <path d="M13.213 9.787a3.39 3.39 0 0 0-4.795 0l-3.425 3.426a3.39 3.39 0 0 0 4.795 4.794l.321-.304m-.321-4.49a3.39 3.39 0 0 0 4.795 0l3.424-3.426a3.39 3.39 0 0 0-4.794-4.795l-1.028.961"/>
      </svg>
      GitHub
    </a>

    <!-- Live Demo Link -->
    <a href="https://sifeditor.website" 
      target="_blank" 
      class="flex items-center gap-1 text-blue-600 underline">
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" 
          viewBox="0 0 24 24" fill="none" stroke="currentColor" 
          stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5">
        <path d="M12 21a9 9 0 1 0 0-18m0 18a9 9 0 1 1 0-18m0 18c2.761 0 3.941-5.163 3.941-9S14.761 3 12 3m0 18c-2.761 0-3.941-5.163-3.941-9S9.239 3 12 3M3.5 9h17m-17 6h17"/>
      </svg>
      Website
    </a>
  </p>

  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const slides = [
  { src: new URL('@/images/dashboard1.png', import.meta.url).href, alt: 'Dashboard sample 1' },
  { src: new URL('@/images/dashboard2.png', import.meta.url).href, alt: 'Dashboard sample 2' },
  { src: new URL('@/images/dashboard3.png', import.meta.url).href, alt: 'Dashboard sample 3' },
  { src: new URL('@/images/dashboard4.png', import.meta.url).href, alt: 'Dashboard sample 4' },
]

const currentSlide = ref(0)
let intervalId = null

function goToSlide(index) {
  currentSlide.value = index
}

function nextSlide() {
  currentSlide.value = (currentSlide.value + 1) % slides.length
}

onMounted(() => {
  intervalId = setInterval(nextSlide, 5000) // auto next every 5s
})

onUnmounted(() => {
  clearInterval(intervalId)
})
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
