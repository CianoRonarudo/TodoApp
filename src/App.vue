<template>
  <!-- Div de la page -->
  <div class="lg:pt-20 h-full w-full bg-slate-800">
    <!-- Titre de la page -->
    <h1 class="text-3xl  text-white text-center font-bold">
      My TodoApp
    </h1>
    <!-- Div de la liste -->

    <div class="flex justify-center items-center flex-col">
      <!-- Nouvelle interface pour l'app -->
      <div class="pt-4 w-1/2">
        <!-- Formulaire d'ajout d'une Todo -->
        <TodoForm :priorities="priorities" @add-todo="addTodo"></TodoForm>
        <!-- Liste des Todo -->
        <div class="w-[100%]">
          <div class="bg-white w-[100%] pb-10 pt-2 px-3 rounded-md">
            <TodoItem v-for="todo in todos" v-bind:key="todo.id" :todo="todo" @todo-change-status="todoChangeStatus(todo)" @delete-todo='deleteTodo(todo)' @edit-todo="editTodo(todo)"></TodoItem>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal pour l'upadate de Todo -->
    <Modal :isOpen="isEdit" @handle-close="closeModal">
      <EditForm @handle-edit-todo="handleEditTodo" :priorities="priorities" :statuses="statuses" :todo="clickTodo"/>
    </Modal>
    
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';
import TodoItem from './components/TodoItem.vue';
import TodoForm from './components/TodoForm.vue';
import Modal from './components/Modal.vue';
import EditForm from './components/EditForm.vue';

const priorities = reactive([
  'High',
  'Low'
])
const statuses = reactive([
  'Active',
  'Completed'
])

const isEdit = ref(false)

const todos = ref(
  [
    { id: 1, text: 'Learn', status: 'Active', priority: 'High', completed: false },
    { id: 2, text: 'Eat', status: 'Completed', priority: 'Low', completed: true },
    { id: 3, text: 'Play guitare', status: 'Active', priority: 'Low', completed: false }
  ]
)
let clickTodo = {}

// Nouvelles fonctions pour les fonctionnalités du TodoApp
const addTodo = (newTodo) => {
  let readyAddTodo = {
    id: todos.value.length + 1,
    text: newTodo.text,
    status: 'Active',
    priority: newTodo.priority,
    completed : false
  }
  todos.value.push(readyAddTodo)
  console.log(todos.value)
}



const deleteTodo = (clickedTodo) => todos.value = todos.value.filter(todo => todo.id !== clickedTodo.id)
function findTodoIndexById(id) {
  return todos.value.findIndex(todo => todo.id === id)
}

const editTodo = (todo) => {
  isEdit.value = !isEdit.value
  clickTodo = { ...todo }
}
const handleEditTodo = (newTodo) => {
  // todos.value[newTodo.id - 1] = newTodo
  let todoIndex = findTodoIndexById(newTodo.id)
  todos.value[todoIndex] = newTodo
  isEdit.value = false
}

const todoChangeStatus = (todo) => todo.status = todo.completed ? 'Completed' : 'Active'

const closeModal = () => {
  isEdit.value = false
}


</script>

<style scoped>

</style>
