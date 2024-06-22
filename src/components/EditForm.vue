/**
 * Ce component est créé pour permettre la souplexe du code de l'app
 * il est crée pour récupérer les valeurs des attributs des todos que 
 * l'utilisateur souhaite modifier.
 * props : 
 * la todo
 * methods :
 * SubmitEditForm :
 * Cette fonction est chargée d'emettre un event de type submit vers le parent (App.vue)
 * @param {}
*/

<template>
    <form @submit.prevent="handleEditTodo" class="pt-8">
        <div>
            <label class="block pb-2" for="text">Name</label>
            <input v-model="newTodo.text" type="text" class="w-[100%] rounded-full py-1 mb-1 px-4 border block" id="text">
        </div>
        <div>
            <label class="block pb-2" for="priority">Priority</label>
            <select v-model="newTodo.priority" class="w-[100%] rounded-full py-1 px-4 mb-1 block">
                <option v-for="priority in props.priorities" :value="priority">{{ priority }}</option>
            </select>
        </div>
        <div>
            <label class="block pb-2" for="priority">Statuses</label>
            <select v-model="newTodo.status" class="w-[100%] rounded-full py-1 px-4 mb-1 block">
                <option v-for="status in props.statuses" :value="status">{{ status }}</option>
            </select>
        </div>
        <div class="flex mt-8 justify-end items-center">
            <input type="submit" class="bg-sky-500 text-white px-6 py-2 rounded-full" value="Save">
        </div>
    </form>
</template>

<script setup>
import { ref } from 'vue';
const props = defineProps(
    [
        "priorities",
        "statuses",
        "todo",
    ]
)
const emit = defineEmits([
    'handle-edit-todo'
])

const newTodo = ref({ ...props.todo })

function handleEditTodo() {
    if (newTodo.value.status === 'Active') {
        newTodo.value.completed = false
    }
    else {
        newTodo.value.completed = true
    }
    emit('handle-edit-todo', newTodo.value)
    
}


</script>

<style lang="scss" scoped>

</style>