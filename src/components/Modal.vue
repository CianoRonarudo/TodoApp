<template>
    
  <Teleport to="body">
    <div v-if="isOpen" class="modal fixed z-[999] top-0 left-1/2 bg-white px-10 py-4">
      <p>Hello from the modal!</p>
      <span @click="handleClose">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
          <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
        </svg>
      </span>
      <!-- <button @click="open = false">Close</button> -->
    </div>
  </Teleport>
</template>

<script setup>
  const props = defineProps([
    'isOpen',
  ])
const emit = defineEmits([
    'handle-close',
  ])

function handleClose() {
  emit('handle-close')
}
</script>

<style scoped>
  /* .modal {
    position: fixed;
    z-index: 999;
    top: 20%;
    left: 50%;
    width: 300px;
    margin-left: -150px;
    padding: 10px;
    background-color: rgb(44, 38, 38);
    color: white;
  } */

</style>