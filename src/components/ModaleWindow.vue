<template>
    <Teleport to="body">
        <div v-if="isOpen" class="modal shadow-2xl rounded-md fixed z-[999] bg-white px-10 py-4 w-[30%]" :class="positionClass">
            <div class="flex justify-end">

                <span class="hover:bg-rose-300 active:bg-rose-600 hover:text-gray-50 rounded-md p-1" @click="handleCloseModal">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-5">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
                    </svg>
                </span>
            </div>
            <div class="h-full flex flex-col content-between">
                
                <slot>
                    
                </slot>
                <!-- <div class="mt-10">
                    <div v-if="modalContent === 'form'" class="flex justify-end py-2 px-1">
                        <button class="font-semibold text-indigo-500 px-2 py-1 rounded-md active:bg-indigo-700 active:text-white">
                            Soumettre
                        </button>
                        <button class="bg-rose-500 font-semibold text-white px-2 py-1 ml-5 rounded-md hover:bg-rose-600  active:bg-rose-700">
                            Retour
                        </button>
                    </div>
                    <div v-else-if="modalContent === 'confirm'">
                        <button class="bg-indigo-600 text-white px-2 py-1">
                            Oui
                        </button>
                        <button class="bg-rose-600 text-white px-2 py-1">
                            Non
                        </button>
                    </div>
                </div> -->
            </div>
        </div>
    </Teleport>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps([
    'isOpen',
    'isRequest',
    'modalContent',
])
console.log(props.modalContent, 'Modal content')

const positionClass = computed(() => {
    return props.isRequest ? "top-10 left-1/3 h-64" : "top-2 left-2 h-36"
})


const emit = defineEmits(['close-modal'])
function handleCloseModal() {
    emit('close-modal')
    
}

</script>

<style lang="scss" scoped>

</style>