<template>
  <dialog id="my_modal_1" class="modal" open>
    <div class="modal-box">
      <h3 class="text-lg font-bold">My CV</h3>
      <!-- Example: embed PDF CV -->
      <iframe src="/path-to-your-cv.pdf" class="w-full h-96"></iframe>

      <div class="modal-action">
        <form method="dialog">
          <button class="btn" @click="$emit('close')">Close</button>
        </form>
      </div>
    </div>
  </dialog>
</template>
