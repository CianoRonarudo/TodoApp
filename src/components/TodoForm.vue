<template>
    <div class="flex flex-col">
        <div class="text-indigo-400 font-bold text-xl mb-3">
            {{ title }}
        </div>
        <div>
            <form @submit.prevent="handleSubmitForm">
                <input required v-model="data.name" :placeholder="title" type="text" class="py-2 rounded-full w-[60%] mr-3 px-5 border focus:outline-none focus:ring focus:ring-indigo-50 text-gray-600">
                <select required v-model="data.priority" name="" id="" class="w-1/3 rounded-full py-2 px-3 bg-white border text-gray-600 focus:outline-none focus:ring focus:ring-indigo-50">
                    <option value="">Priority</option>
                    <option value="High">High</option>
                    <option value="Low">Low</option>
                </select>
                <div class="mt-10">
                    <div class="flex justify-end py-2 px-1">
                        <button type="submit"class="font-semibold text-indigo-500 px-2 py-1 rounded-md active:bg-indigo-700 active:text-white">
                            Soumettre
                        </button>
                        <button type="reset" class="bg-rose-500 font-semibold text-white px-2 py-1 ml-5 rounded-md hover:bg-rose-600  active:bg-rose-700">
                            Effacer
                        </button>
                    </div>
                </div>
            </form>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';


const emit = defineEmits([
    'submit-form',
])

const props = defineProps([
    'isAddForm',
    'todo'
])

let title = props.isAddForm ? 'Ajouter un todo' : 'Editer un todo'
const data = props.isAddForm ? ref({name: '', priority: ''}) : ref( ...props.todo)
const handleSubmitForm = () => {
    // if (data.value.name === '' && data.value.priority === "") {
    //     window.alert('Vous devez remplir le formulaire')
    // }
    emit('submit-form', data.value)
    data.value = {
        name: '',
        priority: ''
    }
}

</script>

<style lang="scss" scoped>

</style>