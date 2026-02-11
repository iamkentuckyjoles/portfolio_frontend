<template>
  <div class="p-4 bg-base-200 rounded-lg shadow-md">
    <h2 class="text-xs font-bold mb-2">contact me</h2>
    <form class="flex flex-col gap-2 text-xs">
      <input type="text" placeholder="your name" class="input input-bordered input-xs" />
      <input type="email" placeholder="your email" class="input input-bordered input-xs" />
      <textarea placeholder="your message" class="textarea textarea-bordered textarea-xs"></textarea>
      <button type="submit" class="btn btn-xs btn-primary mt-2">send</button>
    </form>
  </div>
</template>

<script setup>
// No logic yet — static form
</script>
