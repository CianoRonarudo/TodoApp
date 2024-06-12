<template>
    <div class="border-b grid grid-cols-12 py-2" :class="{'line-through': todo.completed}">
        
        <!-- Partie main de la todo Item -->

        <div class="col-span-1 flex justify-center items-center">
            <input type="checkbox" @change="todoChangeStatus" v-model="todo.completed">
        </div>
        <div class="px-4 col-span-5 flex items-center">
            {{ todo.text }}
        </div>
        <div class="col-span-2 flex justify-center items-center">
            <span class="px-2 py-1 rounded-lg text-xs uppercase" :class="{'bg-sky-500 text-white' : todo.status === 'Active', 'text-yellow-800 bg-yellow-200 bg-opacity-50': todo.status === 'Completed'}" >{{ todo.status }}</span>
            <!-- <span class="text-yellow-800 bg-yellow-200 rounded-lg bg-opacity-50 px-2 py-1 text-xs uppercase" >Completed</span> -->
        </div>
        <div class="col-span-2 flex justify-center items-center">
        <span class="px-2 py-1 rounded-lg text-white text-xs font-bold uppercase" :class="{'bg-red-500': todo.priority === 'High', 'bg-green-500' : todo.priority === 'Low' }">
            {{ todo.priority }}
        </span>
        <!-- <span class="bg-green-500 px-2 py-1 rounded-lg text-white text-xs font-bold uppercase">
            Low
        </span> -->

        </div>

        <!-- Icone de update à cliquer  -->

        <span class="col-span-1 flex justify-center items-center">
            <svg @click="editTodo" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4 hover:text-sky-600">
                <path d="M21.731 2.269a2.625 2.625 0 0 0-3.712 0l-1.157 1.157 3.712 3.712 1.157-1.157a2.625 2.625 0 0 0 0-3.712ZM19.513 8.199l-3.712-3.712-12.15 12.15a5.25 5.25 0 0 0-1.32 2.214l-.8 2.685a.75.75 0 0 0 .933.933l2.685-.8a5.25 5.25 0 0 0 2.214-1.32L19.513 8.2Z" />
            </svg>
        </span>

        <!-- Icone pour la suppression -->

        <span class="col-span-1 flex justify-center items-center">
            <svg @click="deleteTodo" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4 hover:text-red-500">
                <path stroke-linecap="round" stroke-linejoin="round" d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" />
            </svg>
        </span>
    </div>
    
</template>
<script setup>

const props = defineProps(['todo'])
const emit = defineEmits([
    'delete-todo',
    'edit-todo',
    'todo-change-status',
    'todo-change-priority',
])
function deleteTodo() {
    emit('delete-todo', props.todo)
    
    
}
function editTodo() {
    emit('edit-todo')
    console.log("Ready to be updated")
}
function todoChangeStatus() {
    emit('todo-change-status', props.todo )
}
function todoChangePriority() {
    emit('todo-change-priority', props.todo.id)
}
</script>
<style scoped></style>