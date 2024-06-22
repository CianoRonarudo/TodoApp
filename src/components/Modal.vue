<template>
    
  <Teleport to="body">
    <div v-if="isOpen" class="modal shadow-2xl fixed z-[999] top-10 left-1/3 bg-white px-10 py-4 w-[35%] h-96">
      <div class="flex justify-between">
        <p>Titre</p>
        <span class="hover:text-sky-700" @click="handleClose">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-4">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
          </svg>
        </span>
      </div>
      <slot>
        
      </slot>
      <!-- <button @click="open = false">Close</button> -->
    </div>
  </Teleport>
</template>

<script setup>
/*  Liste des props:
  * isOpen: Bool qui sert à l'ouverture et la fermeture de la modale
*/
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