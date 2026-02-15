<template>
  <div class="flex flex-col gap-2 items-end relative">
    <!-- Toggle button (draggable) -->
    <button 
      class="cursor-move absolute bg-transparent border-0 p-0"
      :style="{ top: position.top + 'px', left: position.left + 'px' }"
      @click="toggleChat"
      @mousedown="startDrag"
    >
      <!-- SVG Icon -->
      <svg xmlns="http://www.w3.org/2000/svg" 
          width="24" height="24"
          viewBox="0 0 24 24"
          fill="currentColor"
          :class="props.theme === 'light' ? 'text-black' : 'text-white'">
        <path transform="scale(-1,1) translate(-24,0)"
              fill="currentColor" fill-rule="evenodd"
              d="M12 1.25C6.063 1.25 1.25 6.063 1.25 12c0 1.856.471 3.605 1.3 5.13l-.787 4.233a.75.75 0 0 0 .874.874l4.233-.788A10.7 10.7 0 0 0 12 22.75c5.937 0 10.75-4.813 10.75-10.75S17.937 1.25 12 1.25m5 9.5a1.25 1.25 0 1 0 0 2.5a1.25 1.25 0 0 0 0-2.5M10.75 12a1.25 1.25 0 1 1 2.5 0a1.25 1.25 0 0 1-2.5 0M7 10.75a1.25 1.25 0 1 0 0 2.5a1.25 1.25 0 0 0 0-2.5" 
              clip-rule="evenodd"/>
      </svg>
    </button>

    <!-- Chat container -->
    <div v-if="showChat" 
        class="bg-base-200 rounded-lg shadow-md w-80 absolute text-xs border"
        :style="{ top: position.top + 40 + 'px', left: (position.left - 310) + 'px' }"
        :class="props.theme === 'light' ? 'border-black' : 'border-white'">

      <!-- Header -->
      <div :class="props.theme === 'light' ? 'bg-gray-200 text-black' : 'bg-black text-white'"
           class="flex items-center justify-between px-3 py-2 rounded-t-lg cursor-move"
           @mousedown="startDrag">

        <!-- Profile block -->
        <div class="flex items-center gap-3">
          <div class="relative w-7 h-7 rounded-full overflow-hidden">
            <img 
              :src="props.theme === 'light' ? light : dark" 
              alt="Profile picture" 
              class="w-7 h-7 object-cover transition-opacity duration-300 hover:opacity-0"
            />
            <img 
              :src="props.theme === 'light' ? lightHover : darkHover" 
              alt="Profile hover picture" 
              class="w-7 h-7 object-cover absolute top-0 left-0 opacity-0 hover:opacity-100 transition-opacity duration-300"
            />
          </div>
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
      <div ref="chatContainer" 
           class="p-4 space-y-3 max-h-64 overflow-y-auto scrollbar-hide">
        <div v-for="(msg, index) in messages" :key="index" 
             :class="msg.sender === 'user' ? 'chat chat-end' : 'chat chat-start'">
          
          <!-- Avatar + Name -->
          <div class="chat-image avatar flex items-center gap-2">
            <div class="w-6 h-6 rounded-full overflow-hidden">
              <img
                alt="Avatar"
                :src="msg.sender === 'user' 
                  ? (props.theme === 'light' ? guestLight : guestDark) 
                  : (props.theme === 'light' ? light : dark)"
                class="w-6 h-6 object-cover"
              />
            </div>
          </div>

          <!-- Message bubble -->
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
      <div :class="props.theme === 'light' ? 'bg-gray-200 text-black' : 'bg-black text-white'"
           class="flex gap-2 px-3 py-2 rounded-b-lg">
        <input
          v-model="userInput"
          type="text"
          placeholder="Type your message..."
          class="input input-bordered input-xs w-full font-normal"
          @keyup.enter="sendMessage"
        />
        <button 
          class="btn btn-xs font-normal transition-colors duration-300"
          :class="props.theme === 'light' 
            ? 'bg-white text-black hover:bg-black hover:text-white' 
            : 'bg-black text-white hover:bg-white hover:text-black'"
          @click="sendMessage"
        >
          Send
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, nextTick } from 'vue'
import light from '@/assets/light.png'
import lightHover from '@/assets/light_hover.png'
import dark from '@/assets/dark.png'
import darkHover from '@/assets/dark_hover.png'
import guestLight from '@/assets/guestlight.png'
import guestDark from '@/assets/guestdark.png'

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
const chatContainer = ref(null)

const position = ref({ top: -5, left: -24 })
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

function scrollToBottom() {
  if (chatContainer.value) {
    chatContainer.value.scrollTop = chatContainer.value.scrollHeight
  }
}

async function sendMessage() {
  if (!userInput.value.trim()) return
  messages.value.push({ sender: 'user', text: userInput.value })
  await nextTick()
  scrollToBottom()

  loading.value = true

  try {
    const response = await fetch("http://localhost:8001/api/chat/", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ message: userInput.value })
    })
    const data = await response.json()
    messages.value.push({ sender: 'bot', text: data.response })
    await nextTick()
    scrollToBottom()
  } catch (error) {
    console.error(error)
    messages.value.push({ sender: 'bot', text: "Error connecting to server." })
    await nextTick()
    scrollToBottom()
  } finally {
    loading.value = false
    userInput.value = ""
  }
}
</script>

<style>
/* Hide scrollbar but keep scroll functionality */
.scrollbar-hide::-webkit-scrollbar {
  display: none;
}
.scrollbar-hide {
  -ms-overflow-style: none;  /* IE/Edge */
  scrollbar-width: none;     /* Firefox */
}
</style>
