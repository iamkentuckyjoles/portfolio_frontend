<template>
  <div class="flex flex-col gap-2 items-end relative">
    <!-- Toggle button (draggable) -->
    <button 
      class="flex items-center gap-2 px-3 py-1 rounded text-xs cursor-move whitespace-nowrap absolute"
      :style="{ top: position.top + 'px', left: position.left + 'px' }"
      :class="props.theme === 'light' ? 'bg-black text-white' : 'bg-white text-black'"
      @click="toggleChat"
      @mousedown="startDrag"
    >
      <!-- SVG Icon -->
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16"
           viewBox="0 0 24 24"
           fill="none"
           :class="props.theme === 'light' ? 'text-white' : 'text-black'">
        <g stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
          <path d="M4 4h16v12H5.17L4 17.17V4z"/>
          <circle cx="9" cy="10" r="1"/>
          <circle cx="12" cy="10" r="1"/>
          <circle cx="15" cy="10" r="1"/>
        </g>
      </svg>
      <span class="font-normal"> Kenth</span>
    </button>

    <!-- Chat container -->
    <div v-if="showChat" 
        class="bg-base-200 rounded-lg shadow-md w-80 absolute text-xs border"
        :style="{ top: position.top + 40 + 'px', left: (position.left - 240) + 'px' }"
        :class="props.theme === 'light' ? 'border-black' : 'border-white'">

      <!-- Header -->
    <div :class="props.theme === 'light' ? 'bg-white text-black' : 'bg-black text-white'"
        class="flex items-center justify-between px-3 py-2 rounded-t-lg cursor-move"
        @mousedown="startDrag">

    <!-- Profile block -->
    <div class="flex items-center gap-3">
        <!-- Profile picture with hover swap -->
        <div class="relative w-7 h-7 rounded-full overflow-hidden">
        <!-- Default profile -->
        <img 
            :src="props.theme === 'light' ? light : dark" 
            alt="Profile picture" 
            class="w-7 h-7 object-cover transition-opacity duration-300 hover:opacity-0"
        />
        <!-- Hover profile -->
        <img 
            :src="props.theme === 'light' ? lightHover : darkHover" 
            alt="Profile hover picture" 
            class="w-7 h-7 object-cover absolute top-0 left-0 opacity-0 hover:opacity-100 transition-opacity duration-300"
        />
        </div>

        <!-- Name + status stacked -->
        <div class="flex flex-col">
        <span class="font-semibold text-xs">Kenth Lumantao</span>
        <div class="flex items-center gap-1">
            <span class="w-2 h-2 bg-green-500 rounded-full"></span>
            <span class="text-xs">Online</span>
        </div>
        </div>
    </div>
    </div>


      <!-- Scrollable chat area -->
      <div class="p-4 space-y-3 max-h-40 overflow-y-auto">
        <div v-for="(msg, index) in messages" :key="index" 
             :class="msg.sender === 'user' ? 'chat chat-end' : 'chat chat-start'">
          <div class="chat-image avatar">
            <div class="w-6 rounded-full">
              <img
                alt="Avatar"
                :src="msg.sender === 'user' 
                  ? 'https://img.daisyui.com/images/profile/demo/kenobee@192.webp' 
                  : 'https://img.daisyui.com/images/profile/demo/kenobee@192.webp'"
              />
            </div>
          </div>
          <div class="chat-bubble text-xs font-normal">
            {{ msg.text }}
          </div>
        </div>

        <!-- Loading animation -->
        <div v-if="loading" class="chat chat-start">
          <div class="chat-bubble">
            <span class="loading loading-dots loading-sm"></span>
          </div>
        </div>
      </div>

      <!-- Footer -->
      <div :class="props.theme === 'light' ? 'bg-white text-black' : 'bg-black text-white'"
           class="flex gap-2 px-3 py-2 rounded-b-lg">
        <input
          v-model="userInput"
          type="text"
          placeholder="Type your message..."
          class="input input-bordered input-xs w-full font-normal"
          @keyup.enter="sendMessage"
        />
        <button 
          class="btn btn-xs font-normal"
          :class="props.theme === 'light' ? 'bg-white text-black' : 'bg-black text-white'"
          @click="sendMessage"
        >
          Send
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Import your profile images
import light from '@/assets/light.png'
import lightHover from '@/assets/light_hover.png'
import dark from '@/assets/dark.png'
import darkHover from '@/assets/dark_hover.png'

const props = defineProps({
  theme: {
    type: String,
    default: 'light'
  }
})

const showChat = ref(false)
const loading = ref(false)
const messages = ref([
  { sender: 'bot', text: "Hello, I'm Kenth Chatbot. Ask me anything about Kenth and I’ll share what I know, as long as I have the knowledge." }
])
const userInput = ref("")

const position = ref({ top: -33, left: -140})
let dragging = false
let offsetX = 0
let offsetY = 0

function toggleChat() {
  showChat.value = !showChat.value
}

function startDrag(event) {
  dragging = true
  offsetX = event.clientX - position.value.left
  offsetY = event.clientY - position.value.top
  document.addEventListener('mousemove', onDrag)
  document.addEventListener('mouseup', stopDrag)
}

function onDrag(event) {
  if (!dragging) return
  position.value = {
    top: event.clientY - offsetY,
    left: event.clientX - offsetX
  }
}

function stopDrag() {
  dragging = false
  document.removeEventListener('mousemove', onDrag)
  document.removeEventListener('mouseup', stopDrag)
}

async function sendMessage() {
  if (!userInput.value.trim()) return
  messages.value.push({ sender: 'user', text: userInput.value })
  loading.value = true

  try {
    const response = await fetch("/api/chat/", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ message: userInput.value })
    })
    const data = await response.json()
    messages.value.push({ sender: 'bot', text: data.response })
  } catch (error) {
    console.error(error)
    messages.value.push({ sender: 'bot', text: "Error connecting to server." })
  } finally {
    loading.value = false
    userInput.value = ""
  }
}
</script>
