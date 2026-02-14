<template>
  <div class="p-4 text-left">
    <!-- Name + settings icon -->
    <!-- Name + check + settings -->
    <div class="flex items-center justify-between">
      <div class="flex items-start gap-2">
        <h1 class="text-xl font-bold text-blue-600">Kenth Lumantao</h1>
        <!-- Check SVG beside Lumantao -->
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" 
            viewBox="0 0 24 24" class="text-blue-600">
          <path fill="none" stroke="currentColor" stroke-linecap="round" 
                stroke-linejoin="round" stroke-width="2" 
                d="m15 10l-4 4l-2-2m4.246-8.541l1.221 1.04c.308.262.69.42 1.092.453l1.6.128a1.92 1.92 0 0 1 1.761 1.76l.127 1.6c.033.403.192.786.454 1.093l1.04 1.22a1.92 1.92 0 0 1 0 2.492l-1.04 1.221c-.262.308-.421.69-.453 1.093l-.128 1.6a1.92 1.92 0 0 1-1.76 1.761l-1.6.128a1.92 1.92 0 0 0-1.093.452l-1.221 1.04a1.92 1.92 0 0 1-2.492 0l-1.22-1.04a1.92 1.92 0 0 0-1.094-.452l-1.6-.128a1.92 1.92 0 0 1-1.76-1.762l-.128-1.599a1.92 1.92 0 0 0-.453-1.092l-1.04-1.222a1.92 1.92 0 0 1 0-2.49l1.04-1.222c.263-.308.42-.69.452-1.093l.128-1.599A1.92 1.92 0 0 1 6.842 5.08l1.598-.127A1.92 1.92 0 0 0 9.533 4.5l1.221-1.04a1.92 1.92 0 0 1 2.492 0"/>
        </svg>
      </div>
    </div>

    <!-- Location with icon -->
    <p class="mt-2 text-xs flex items-center gap-2">
      <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" 
          viewBox="0 0 24 24" fill="currentColor">
        <path d="M19 9A7 7 0 1 0 5 9c0 1.387.409 2.677 1.105 3.765h-.008L12 22l5.903-9.235h-.007A6.97 6.97 0 0 0 19 9m-7 3a3 3 0 1 1 0-6a3 3 0 0 1 0 6"/>
      </svg>
      Philippines
    </p>

    <p class="mt-2 text-sm font-semibold">
      A{{ displayedText }}
    </p>




   
     
    <!-- Send a mail + Socials inline -->
    <div class="mt-2 flex flex-row items-center gap-6 text-xs">
      
      <!-- Send a mail + SVG grouped tightly -->
      <div class="flex items-center">
        <span class="text-xs"></span>
        <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" 
            viewBox="0 0 256 256" class="cursor-pointer" @click="showModal = true">
          <g fill="none">
            <rect width="256" height="256" rx="60"/>
            <path fill="#4285f4" d="M41.636 203.039h31.818v-77.273L28 91.676v97.727c0 7.545 6.114 13.636 13.636 13.636"/>
            <path fill="#34a853" d="M182.545 203.039h31.819c7.545 0 13.636-6.114 13.636-13.636V91.675l-45.455 34.091"/>
            <path fill="#fbbc04" d="M182.545 66.675v59.091L228 91.676V73.492c0-16.863-19.25-26.477-32.727-16.363"/>
            <path fill="#ea4335" d="M73.455 125.766v-59.09L128 107.583l54.545-40.909v59.091L128 166.675"/>
            <path fill="#c5221f" d="M28 73.493v18.182l45.454 34.091v-59.09L60.727 57.13C47.227 47.016 28 56.63 28 73.493"/>
          </g>
        </svg>
      </div>

      <!-- Modal -->
      <div v-if="showModal" 
          class="fixed inset-0 flex items-center justify-center 
                  bg-black/40 backdrop-blur-sm z-50 
                  animate-fadeIn">
        <div class="bg-white dark:bg-base-200 p-6 rounded shadow-md w-80 
                    transform animate-slideUp">
          <h2 class="text-sm font-bold mb-2">Send a Mail</h2>
          <form @submit.prevent="submitForm">
            <input type="text" v-model="form.name" placeholder="Name" 
                  class="input input-sm input-bordered w-full mb-2" />
            <input type="email" v-model="form.email" placeholder="Email" 
                  class="input input-sm input-bordered w-full mb-2" />
            <textarea v-model="form.message" placeholder="Message" 
                      class="textarea textarea-sm textarea-bordered w-full mb-2"></textarea>
            <div class="flex justify-end gap-2">
              <button type="button" class="btn btn-sm" @click="showModal = false">Cancel</button>
              <button type="submit" class="btn btn-sm btn-primary">Send</button>
            </div>
          </form>
        </div>
      </div>
    
      <!-- Social icons inline -->
      <div class="flex items-center flex-row gap-2">
     

      <!-- Social icons inline -->
      <div class="flex flex-row gap-2">
        <!-- Facebook -->
        <a href="https://facebook.com/sample" target="_blank" class="text-blue-600">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" 
              viewBox="0 0 16 16" fill="currentColor">
            <path d="M8 0a8 8 0 0 1 1.083 15.927v-5.755h2.07l.326-2.113H9.083V6.903c0-.829.255-1.57.971-1.65l.132-.007h1.313V3.401l-.291-.036c-.28-.03-.711-.064-1.35-.064c-1.86 0-2.978.956-3.05 3.123l-.004.228V8.06H4.825v2.113h1.98v5.74A8.002 8.002 0 0 1 8 0"/>
          </svg>
        </a>


        <!-- LinkedIn -->
        <a href="https://linkedin.com/in/sample" target="_blank" class="text-blue-600">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" 
              viewBox="0 0 1536 1536" fill="currentColor">
            <path d="M237 1286h231V592H237zm246-908q-1-52-36-86t-93-34t-94.5 34t-36.5 86q0 51 35.5 85.5T351 498h1q59 0 95-34.5t36-85.5m585 908h231V888q0-154-73-233t-193-79q-136 0-209 117h2V592H595q3 66 0 694h231V898q0-38 7-56q15-35 45-59.5t74-24.5q116 0 116 157zm468-998v960q0 119-84.5 203.5T1248 1536H288q-119 0-203.5-84.5T0 1248V288Q0 169 84.5 84.5T288 0h960q119 0 203.5 84.5T1536 288"/>
          </svg>
        </a>



        <!-- GitHub -->
        <a href="https://github.com/sample" target="_blank" class="text-blue-600">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" 
              viewBox="0 0 1536 1536" fill="currentColor">
            <path d="M519 1072q4-6-3-13q-9-7-14-2q-4 6 3 13q9 7 14 2m-28-41q-5-7-12-4q-6 4 0 12q7 8 12 5q6-4 0-13m-41-40q2-4-5-8q-7-2-8 2q-3 5 4 8q8 2 9-2m21 23q2-1 1.5-4.5t-3.5-5.5q-6-7-10-3t1 11q6 6 11 2m86 75q2-7-9-11q-9-3-13 4q-2 7 9 11q9 3 13-4m42 3q0-8-12-8q-10 0-10 8t11 8t11-8m39-7q-2-7-13-5t-9 9q2 8 12 6t10-10m642-317q0-212-150-362T768 256T406 406T256 768q0 167 98 300.5T606 1254q18 3 26.5-5t8.5-20q0-52-1-95q-6 1-15.5 2.5t-35.5 2t-48-4t-43.5-20T468 1073q-23-59-57-74q-2-1-4.5-3.5l-8-8l-7-9.5l4-7.5L415 967q6 0 15 2t30 15.5t33 35.5q16 28 37.5 42t43.5 14t38-3.5t30-9.5q7-47 33-69q-49-6-86-18.5t-73-39t-55.5-76T441 741q0-79 53-137q-24-62 5-136q19-6 54.5 7.5T614 505l26 16q58-17 128-17t128 17q11-7 28.5-18t55.5-26t57-9q29 74 5 136q53 58 53 137q0 57-14 100.5t-35.5 70T992 956t-62.5 26t-68.5 12q35 31 35 95q0 40-.5 89t-.5 51q0 12 8.5 20t26.5 5q154-52 252-185.5t98-300.5m256-480v960q0 119-84.5 203.5T1248 1536H288q-119 0-203.5-84.5T0 1248V288Q0 169 84.5 84.5T288 0h960q119 0 203.5 84.5T1536 288"/>
          </svg>
        </a>


        <!-- Twitter/X -->
        <a href="https://twitter.com/sample" target="_blank" class="text-blue-600">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" 
              viewBox="0 0 24 24">
            <path fill="currentColor" fill-rule="evenodd" 
                  d="M5 1a4 4 0 0 0-4 4v14a4 4 0 0 0 4 4h14a4 4 0 0 0 4-4V5a4 4 0 0 0-4-4zm-.334 3.5a.75.75 0 0 0-.338 1.154l5.614 7.45l-5.915 6.345l-.044.051H6.03l4.83-5.179l3.712 4.928a.75.75 0 0 0 .337.251h4.422a.75.75 0 0 0 .336-1.154l-5.614-7.45L20.017 4.5h-2.05l-4.83 5.18l-3.714-4.928a.75.75 0 0 0-.337-.252zm10.88 13.548L6.431 5.952H8.45l9.114 12.095z" 
                  clip-rule="evenodd"/>
          </svg>
        </a>

      </div>
    </div>
  </div>
</div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const showModal = ref(false)
const form = ref({ name: '', email: '', message: '' })

function submitForm() {
  console.log('Form submitted:', form.value)
  showModal.value = false
}

// Typewriter animation for "Aspiring Full Stack Dev"
const fullText = "spiring Full Stack Developer"
const displayedText = ref("")
let index = 0
let intervalId = null

onMounted(() => {
  intervalId = setInterval(() => {
    if (index < fullText.length) {
      displayedText.value += fullText[index]
      index++
    } else {
      clearInterval(intervalId)
    }
  }, 100) // 100ms per letter
})

onUnmounted(() => {
  if (intervalId) clearInterval(intervalId)
})
</script>
